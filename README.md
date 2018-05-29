# springboot-amqp
##1、RabbitMQ自定义配置

###（1）、配置文件application.properties中进行自定义属性的配置
```yml
    spring:
      rabbitmq:
        username: rabbitAdmin
        password: 123456789
    #    支持发布确认
        publisher-confirms: true
    #    支持发布返回
        publisher-returns: true
        listener:
          simple:
    #      采用手动应答
            acknowledge-mode: manual
    #        当前监听容器数
            concurrency: 1
    #        最大数
            max-concurrency: 1
    #        是否支持重试
            retry:
              enabled: true
```
###（2）、自定义CachingConnectionFactory，设置连接的相关属性
```java
    @Bean
    @ConfigurationProperties(prefix = "spring.rabbitmq")
    public CachingConnectionFactory connection(){
        CachingConnectionFactory connectionFactory=new CachingConnectionFactory();
        connectionFactory.setHost("127.0.0.1");
        connectionFactory.setPort(5672);
        connectionFactory.setVirtualHost("/vhost_mmr");
        connectionFactory.setUsername("user_mmr");
        connectionFactory.setPassword("123");
        return connectionFactory;
    }
```
###（3）、自定义RabbitTemplate模板
