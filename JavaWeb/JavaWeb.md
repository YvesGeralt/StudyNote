# JavaWeb

## Back-end
 >后端，是接受前端请求(request)，并提供数据服务的部分(response)。通常包含Server和数据库。我们必须对计算机编程，才能让他成为一台服务器。

- ### Backend Programming Language
  要编写后端程序，首先需要后端编程语言，现在最热门的后端语言是：
  - JaveScript(NodeJS)
  - Ruby
  - Python
  - Goland
  - Java

- ### Backend Framework<br>
  直接使用后端编程语言来编写后端程序，十分困难且混乱，而且需要大量的代码，所以我们需要后端框架来帮我们解决问题，对应每种后端语言都有常见的后端框架：
  - Express for NodeJs
  - Django/Flask for python
  - Rails for Ruby
  - Gin for Goland
  - Spring for Java

- ### Backend Package<br>
  在此之外，对于一些热门的功能例如计算、与数据库通信以及设置用户登录和身份验证，已经有前人写过功能完善的代码，这些代码被成为包(Package)。为了安装和管理这些包，我们使用包管理器，每种后端语言都有自己的包管理器：
  - npm for NodeJS
  - pip for python
  - bundler for Ruby
  - Go mod for Goland
  - Maven for Java
  
- ### Database<br>
  数据库用于存储软件/网站所需的各种信息，通常情况下，数据库和服务器是运行在不同计算机上的软件，我们必须进行一些设置，以便后端和数据库连接。常见的数据库有：
  - 关系型数据库
    - MySQL
    - PostgreSQL
    - Oracle
  - 非关系型数据库
    - Redis:键值形
    - MongoDB:文档形
    - HBase:列族形
    - Neo4j:图数据库

- ### Request<br>
  下面是一个常见的Request示例：
  ```
  Post https://amazon.com/orders

  {
    "order": [
       {
          "id": "037d0156",
          "name": "Adidas Shoes",
          "quantity": 1
       },
       {
          "id": "994c97a1",
          "name": "Amazon Essential Socks",
          "quantity": 2
       }
    ],

    "paymentMethod": "creditCard1",
    "deliveryAddress": "address1",
    ...
  }
  ```
  可以看到，一个Request请求通常由一下及部分组成：
  - 请求行
    - HTTP方法，如POST、GET、DELETE
    - 请求URL
    - HTTP版本
  - 请求头<br>
    包含元数据，用于描述请求特性和客户端环境
  - 请求体<br>
    一般是POST请求发送的表单数据

- ### REST API<br>
  在后端，我们使用编程语言和后端框架来定义允许哪些类型的请求，并处理请求：
  ```
  app.post('/orders', (request, response) => {
    const order = createOrder(request);
    database.save(order);
    response.send('Order confirmed.');
  });

  app.get('/orders', (request, response) => {
    const orderes = database.getOrderHistory();
    response.json(orders);
  });

  app.delete('/orders/:id', (request, response) => {
    database.cancelOrder(request);
    response.json('Order canceled.');
  });

  app.use((request, response) => {
    response.send('Error: not allowed.');
  });
  ```
  像这样，后端允许所有不同类型的请求的列表，叫做API。像这样用HTTP方法和URL路径`post/orders`来识别请求的行为，称为**REST**。REST命名约定的API称为**Rest api**。

- ### Cloud Computing<br>
  - Infrastructure<br>
    公司不是购买自己的计算机来运行网站，而是从云计算公式租用计算机。云计算的根本思想是租用服务器，这被称为**IaaS**即基础设施即服务。
  - Platform<br>
    租用提供云计算公司的计算机，实际上是租用一个巨型计算机中的虚拟机来运行我们的后端和数据库。当访问量增多时，我们可以租用多个虚拟机运行相同的后端代码，并另外设置一台特殊的虚拟机，称为负载均衡器，来均匀分配对不同虚拟机的请求。<br>
    云计算公司提供一种叫**PaaS**的服务，我们只需要上传后端代码，它将设置所有虚拟机包括负载均衡器，帮我们集成一切，称作平台即服务
  - Software<br>
    当我们的网站有很多功能时，代码量也将变得巨大。我们可以将各个功能分开，每个功能的代码称为一个代码库，每个代码库都有单独的后端、负载均衡器甚至是数据库。代码库之间通过请求联系，这被称为**微服务**<br>
    有些公司提供了某种微服务的后端和API，因此我们可以直接使用这个公司的后端和API，不需要自己编写这个微服务的后端。这被称为**SaaS**,软件即服务。

- ### Addition Technology<br>
  - 存储技术<br>
    - CDN 图像存储数据库
    - Elastic Search 搜索数据库
    - Redis 缓存
    - Snowflack 分析数据库
  - 消息队列<br>
    进程间通信和同一进程不同线程间的通信方式<br>
    MQ应用场景：异步处理、应用解耦、流量削峰、消息通讯<br>
    MQ使用总结：计算结果不要求立刻返回给发送者，如日志服务、业务监控服务