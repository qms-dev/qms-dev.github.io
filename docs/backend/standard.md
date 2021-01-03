---
layout: default
title: QMOJ后端开发规范
parent: 后端文档
nav_order: 2
---

# QMOJ后端开发规范

> 第一，绝不意气用事

## 整体的 

1. 安装`lombok`插件

2.  安装阿里巴巴开发规范插件

3.  `vo`这个包是与前端打交道的，接收前端的请求体和传给前端

4.  `dto`是`vo->entity`转换过程中可能需要的 

5. `config`写配置参数文件的(`redis` `druid`等配置) 

6.  `enums`写状态，各种枚举类都放这

7.  `utils`工具类

8.  `common`与`utils`的区别区分下，全局异常处理，统一返回类等等，都可以放到`common`

9.  `pojo`额外的实体写这里吧

10. `exception`自定义异常 `controller`层 

    

## 注意事项

1. 尽量不要异常处理，不要写业务逻辑，不要写日志 

2. 方法名记得加上`@Api`，如果有字段加上`@ApiParam`

3. 方法上面不用加注解

4. 统一`rest`风格

5. 类上面加个 例如`HelloController` 加上 `/hello`

6. `Autowired`注解下面加上`private` 

7. `service层`接口记得写上注释，写详细更好 

8. `impl`包中带有`@Override`注解的实现接口就不建议写注释了 

9. `dao`层`springData JPA`学习视频：https://www.bilibili.com/video/BV1Z64y1o7ap?from=search&seid=14261966763838821307 直接从40视频开始看，一共要不了多长时间

——by 规则制定者：**Twilight**