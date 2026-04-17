# .NET → Java 简历技术栈对应关系

> 基于简历内容，逐项列出 .NET 与 Java 生态的对应关系，方便面试时快速切换表述

---

## 一、框架与运行时

| .NET 技术 | Java 对应 | 说明 |
|-----------|-----------|------|
| .NET Core / .NET Framework | JDK 8+ / JDK 17+ | 运行时/基座框架 |
| ASP.NET Core Web API | Spring Boot + Spring MVC | RESTful API 开发 |
| ASP.NET MVC | Spring MVC（传统） | MVC 模式 Web 开发 |
| .NET 10 | JDK 17 / JDK 21 | 最新 LTS 版本 |
| Program.cs 启动配置 | Application.java + application.yml | 启动入口与配置 |
| Middleware（中间件） | Filter / Interceptor | 请求管道拦截 |
| Dependency Injection（内置） | Spring IoC / @Autowired | 依赖注入 |

---

## 二、微服务与网关

| .NET 技术 | Java 对应 | 说明 |
|-----------|-----------|------|
| 自研微服务方案 | Spring Cloud（全家桶） | 微服务框架 |
| Nacos（注册/配置） | Nacos / Consul / Eureka | 服务注册与配置中心 |
| YARP / 自研网关 | Spring Cloud Gateway | API 网关 |
| Polly 熔断 | Sentinel / Resilience4j | 熔断降级 |
| Refit | OpenFeign / LoadBalancer | 声明式 HTTP 客户端 |
| 自研服务间调用 | OpenFeign + Ribbon/LoadBalancer | 服务间 RPC |
| 配置热更新 | Nacos Config + @RefreshScope | 配置动态刷新 |

---

## 三、ORM 与数据访问

| .NET 技术 | Java 对应 | 说明 |
|-----------|-----------|------|
| EF Core | JPA / Hibernate | ORM 框架 |
| Dapper | MyBatis | 轻量级 SQL 映射 |
| SqlSugar | MyBatis-Plus | 增强 ORM（代码生成/分页/租户插件等） |
| LINQ | Stream API / MyBatis-Plus Wrapper | 集合查询语法 |
| EF Core Include | MyBatis-Plus 关联查询 / @TableField | 关联加载 |
| Code First | JPA @Entity + ddl-auto | 数据库优先/代码优先 |
| Migration | Flyway / Liquibase | 数据库版本迁移 |

---

## 四、数据库

| .NET 技术 | Java 对应 | 说明 |
|-----------|-----------|------|
| SQL Server（主力） | MySQL（主力） | 关系型数据库 |
| Oracle | Oracle | 关系型数据库 |
| MongoDB（C# Driver） | MongoDB（Spring Data MongoDB） | 文档数据库 |
| 分库分表（手写） | ShardingSphere | 分库分表中间件 |
| 读写分离（手写） | MyBatis-Plus 动态数据源 / ShardingSphere | 读写分离 |
| SqlSugar 租户过滤器 | MyBatis-Plus TenantLineInnerInterceptor | 多租户 SQL 拦截 |

---

## 五、缓存与消息

| .NET 技术 | Java 对应 | 说明 |
|-----------|-----------|------|
| StackExchange.Redis | RedisTemplate / Lettuce / Jedis | Redis 客户端 |
| Redis 滑动窗口 | Redis + Lua 脚本滑动窗口 | 分布式限流 |
| Redis SETNX | Redis SETNX / Redisson | 分布式锁/幂等 |
| Redis Pub/Sub | Redis Pub/Sub / RocketMQ | 跨节点消息广播 |
| RabbitMQ（.NET Client） | RabbitMQ / RocketMQ | 消息队列 |
| RedLock.net | Redisson | 分布式锁 |

---

## 六、流程引擎

| .NET 技术 | Java 对应 | 说明 |
|-----------|-----------|------|
| Workflow Core | Flowable / Activiti | 工作流引擎 |
| 节点配置 | BPMN 2.0 建模 | 流程定义标准 |
| 审批流代码配置 | Flowable API / BPMN XML | 流程配置方式 |

---

## 七、任务调度与日志

| .NET 技术 | Java 对应 | 说明 |
|-----------|-----------|------|
| Hangfire | XXL-Job / Quartz | 任务调度 |
| Serilog | Logback / SLF4J + Logstash | 日志框架 |
| 自建批处理 | Spring Batch / XXL-Job | 批处理框架 |

---

## 八、接口文档与校验

| .NET 技术 | Java 对应 | 说明 |
|-----------|-----------|------|
| Swagger（Swashbuckle） | Swagger / Knife4j | 接口文档 |
| Data Annotations | JSR-303 / Hibernate Validator | 参数校验 |
| FluentValidation | 自定义 Validator | 复杂校验 |

---

## 九、桌面开发 → Web 迁移

| .NET 技术 | Java 对应 | 说明 |
|-----------|-----------|------|
| WPF + MVVM | Vue3 + Element Plus | 桌面 → Web 前端 |
| CommunityToolkit.Mvvm | Pinia + Vue3 Composition API | 状态管理/MVVM |
| WinForms | — | 桌面端（Java 侧不常用，简历中弱化） |
| System.IO.Ports | jSerialComm | 串口通信 |

---

## 十、DevOps 与部署

| .NET 技术 | Java 对应 | 说明 |
|-----------|-----------|------|
| Docker + .NET 镜像 | Docker + OpenJDK 镜像 | 容器化 |
| Jenkins Pipeline | Jenkins Pipeline | CI/CD |
| Helm + K8s | Helm + K8s | 容器编排 |
| Nginx 反向代理 | Nginx 反向代理 | 负载均衡 |

---

## 十一、简历项目对应速查

| 简历项目 | .NET 技术栈 | Java 技术栈 |
|----------|-------------|-------------|
| 专家培训与考试系统 | .NET 10 + Redis + Workflow Core + Polly | Spring Boot + Spring Cloud + Redis + Flowable + Sentinel |
| 多租户电子发票网关 | .NET 10 + MongoDB + 工厂模式 | Spring Boot + MongoDB + 工厂模式 + Spring Cloud Gateway |
| HDIS 血液透析 SaaS | ASP.NET Core + Admin.NET + SqlSugar | Spring Boot + Spring Cloud + MyBatis-Plus + Nacos |
| HIS 药房模块 | WPF + WinForms + 串口通信 | Spring Boot + Vue3 + jSerialComm |
| 金融保函系统 | 工厂+策略模式 + SM4 | 工厂+策略模式 + SM4（Hutool 加解密） |
| API 网关 | ASP.NET Core + Refit | Spring Cloud Gateway + OpenFeign |
| ETL 数据平台 | Hangfire + Serilog | XXL-Job + Logback |
| IOT 设备采集 | WinForms + 串口 + CEF | Spring Boot + jSerialComm + 内嵌前端 |

---

## 十二、面试话术转换建议

1. **不要说**"我在 .NET 里用 SqlSugar"，**要说**"我用 MyBatis-Plus 做数据访问，和 SqlSugar 思路类似"
2. **不要说**"Polly 熔断"，**要说**"Sentinel 做熔断降级，思路和 Polly 一致，按规则配置降级策略"
3. **不要说**"Workflow Core"，**要说**"Flowable/Activiti 实现审批流，支持 BPMN 2.0 标准建模"
4. **不要过度强调桌面端经验**，Java 岗位更看重 Web 和微服务，药房模块重点讲业务逻辑和设备对接
5. **突出 Spring Cloud 全家桶**：Gateway、Nacos、OpenFeign、Sentinel 是 Java 岗必备关键词
