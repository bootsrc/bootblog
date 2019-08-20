
类DefaultConfigImpl在Spring Bean容器里已经被注册了并且初始化完毕了。这时候怎么去修改DefaultConfigImpl的bean实例里的method内容？

答案: 

BeanPostProcessor是Spring Bean的统一后置处理器。 也就是在所以的bean被初始化并注册到bean容器后，统一都会经过一些BeanPostProcessor的处理。

我们只需要@Bean或者@Component注册这个MyBeanPostProcessor就可以统一处理,用自己的bean去替换指定的bean。这样实际使用的bean的field和method都可以被替换掉.

```java
public class MyConfigImpl extends DefaultConfigImpl implements BeanPostProcessor {
 
    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName)
	throws BeansException {
        return bean;
    }
 
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName)
	throws BeansException {
        if (beanName.equals("defaultcfg")) {
            // do something
            return this;
        }
        return bean;
    }
}
```


参考文档 [链接](https://mp.weixin.qq.com/s?__biz=MzAxMjY1NTIxNA==&mid=2454441975&idx=1&sn=98cc876419085419bd1c58b06f7b8a71&chksm=8c11e0f6bb6669e04026193980d51dc3f952e2aef374d6af8558c57c01981e3921c779a60cec&scene=21#wechat_redirect)

Demo如下:

```java
/**
 * 定义一个前置后置处理器
 *
 * @author zhangqh
 * @date 2018年5月6日
 */
public class MyBeanPostProcessor implements BeanPostProcessor {
    public Object postProcessBeforeInitialization(Object bean, String beanName)
            throws BeansException {
        // 这边只做简单打印   原样返回bean
        System.out.println("postProcessBeforeInitialization===="+beanName);
        return bean;
    }
    public Object postProcessAfterInitialization(Object bean, String beanName)
            throws BeansException {
        // 这边只做简单打印   原样返回bean
        System.out.println("postProcessAfterInitialization===="+beanName);
        return bean;
    }
}
```
配置类中增加配置如下：
```java
@Bean
public MyBeanPostProcessor getMyBeanPostProcessor(){
    return new MyBeanPostProcessor();
}
```
运行测试结果如下：
```text

postProcessBeforeInitialization====org.springframework.context.event.internalEventListenerProcessor
postProcessAfterInitialization====org.springframework.context.event.internalEventListenerProcessor
postProcessBeforeInitialization====org.springframework.context.event.internalEventListenerFactory
postProcessAfterInitialization====org.springframework.context.event.internalEventListenerFactory
postProcessBeforeInitialization====user1
postProcessAfterInitialization====user1

```
