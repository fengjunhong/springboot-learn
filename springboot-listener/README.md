# 在Spring框架中提供了两种事件监听的方式：

1. 编程式：通过实现ApplicationListener接口来监听指定类型的事件
   
    * 发布：应用上下文AbstractApplicationContext实际还是通过继承ApplicationEventPublisher接口，实现了其中的事件发布的方法，使得Spring应用上下文有了发布事件的功能，在AbstractApplicationContext内部通过SimpleApplicationEventMulticaster事件发布类，将具体事件ApplicationEvent发布出去。
    * 监听：SimpleApplicationEventMulticaster.java中尝试将当前事件逐个广播到指定类型的监听器中（listeners已经根据当前事件类型过滤了）
2. 注解式：通过在方法上加@EventListener注解的方式监听指定参数类型的事件，写该类需要托管到Spring容器中
    * @EventListener注解主要通过EventListenerMethodProcessor扫描出所有带有@EventListener注解的方法，然后动态构造事件监听器，并将监听器托管到Spring应用上文中。
3. 通过application.properties中配置context.listener.classes属性指定监听器
    * 类DelegatingApplicationListener，该类的作用是从application.properties中读取配置context.listener.classes，并将事件广播给这些配置的监听器。
    
    
# Reference
https://www.cnblogs.com/duanxz/p/11243271.html