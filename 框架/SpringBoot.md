### SpringBoot优缺点：

#### 优点：

* 快速构建项目
* 对主流开发框架的无配置集成
* 项目可独立运行，无需外部依赖 Servlet 容器
* 提供运行时的应用监控
* 极大地提高了开发、部署效率
* 与云计算的天然集成
### 缺点：

* 版本迭代速度很快，一些模块改动很大
* 由于不用自己做配置，报错时很难定位
* 网上现成的解决方案比较少
### SpringBoot启动了流程的三部分：

1. 第一部分进行SpringApplication的初始化模块，配置一些基本的环境变量、资源、构造器、监听器；
2. 第二部分实现了应用具体的启动方案，包括启动流程的监听模块、加载配置环境模块、及核心的创建上下文环境模块；
3. 第三部分是自动化配置模块，该模块作为springboot自动配置核心，在后面的分析中会详细讨论。在下面的启动程序中我们会串联起结构中的主要功能。

