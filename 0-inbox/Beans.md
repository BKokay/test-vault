```java
public class SampleBean {
  public void init() { // initialization logic }
  public void destroy() { // destruction logic }
  // bean code
}
public interface BeanInterface {
  // interface code
}
public class BeanInterfaceImpl implements BeanInterface
                {
  // bean code
}
@Configuration
public class AppConfig {
  @Bean(initMethod = "init", destroyMethod = "destroy",
    name = {"sampleBean", "sb"}")
  @Description("Demonstrate a simple bean")
  public SampleBean sampleBean() {
    return new SampleBean();
  }
  @Bean
  public BeanInterface beanInterface() {
    return new BeanInterfaceImpl();
  }
}
```