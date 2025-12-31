# CRUD

> CRUD，指的就是后端业务中的增删查改，是后端开发最基本，也是必须熟练掌握的业务技能。我将结合这几天苍穹外卖的开发实战经验，总结在Spring Boot框架下常见的CRUD操作

我们的一个后端项目一半由三个模块组成:`common`、`pojo`、`server`。<br>
1. `common`模块包含项目中多个模块都会用到的公共组件和工具，比如`constants`(常量类),`Utils`(工具类),`exception`(异常类)等<br>
2. `pojo`模块包含数据模型和传输对象，比如`DTO`(数据传输对象),`entity`(数据库实体类),`VO`(视图对象)<br>
3. `server`模块包含处理业务的代码，核心是`controller`(控制层),`service`(业务逻辑层),`mapper`(数据访问层/持久层)，此外还有`annotation`(自定义注解),`aspect`(AOP切面),`config`(配置类)等,以及项目启动类`Application`和配置文件`application.yml`

- POST
  - 新增<br>
    1. controller层:获取DTO对象，调用service层，返回`Result.success()`<br>
    2. service层:将DTO对象转化为entity对象，(使用`BeanUtils.copyProperties`来拷贝属性),调用mapper层，传入entity对象。
    3. mapper层:如果数据库逻辑操作简单，直接在注解编写SQL语句，若复杂则在xml文件中用标签语句编写
  - 文件上传
    1. controller层:获取file对象,调用ali云工具，将文件上传至云端，返回文件存储路径，使图片回显
- GET
  - 分页查询<br>
    1. controller层:使用MyBatis的分页插件pageHelper,获取PageQueryDTO对象，返回`Result.success(pageResult)`<br>
    2. service层:使用`PageHelper.startPage(PageQueryDTO.getPage()/页码,PageQuerryDTO.getPageSize()/每页几条数据)`来进行分页，定义`page`来接受mapper层操作后传来的对象(如果字段涉及多张表，使用VO作为Page的泛型)<br>
    3. mapper层:在xml文件中编写SQL语句，涉及模糊查询`name like concat('%',#{name},'%')`
- PUT
  - 更新(逻辑类似新增)
    1. controller层:获取DTO对象，调用service层，返回`Result.success()`
    2. service层:将DTO对象转化为entity对象，(使用`BeanUtils.copyProperties`来拷贝属性),调用mapper层，传入entity对象。如果不好处理，可分为删除原有数据和插入新数据
    3. mapper层:在xml文件中编写SQL语句，包含所有可能更新的数据，若非空则更新
- DELETE
  - 批量删除
    1. controller层:获取ids参数,调用service层，返回`Result.success()`
    2. service层:定义不能删除的情况，抛出异常，调用mapper层
    3. mapper层:在xml文件中编写SQL语句<br>
       ```
        <delete id="deleteByIds">
            delete from dish where id in 
            <foreach collection="ids" open="(" close=")" separator="," item="id">
                #{id}
            </foreach>
        </delete>
       ```
