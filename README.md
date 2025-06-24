package com.example.lifecycle;

import jakarta.annotation.PostConstruct;
import jakarta.annotation.PreDestroy;
import org.springframework.beans.factory.DisposableBean;
import org.springframework.beans.factory.InitializingBean;
import org.springframework.stereotype.Component;

@Component
public class LifeCycleBean implements InitializingBean, DisposableBean {

    public LifeCycleBean() {
        System.out.println("Constructor: LifeCycleBean object created.");
    }

    @PostConstruct
    public void postConstruct() {
        System.out.println("@PostConstruct: Initialization logic after bean creation.");
    }

    @Override
    public void afterPropertiesSet() {
        System.out.println("afterPropertiesSet(): Called after setting bean properties.");
    }

    @PreDestroy
    public void preDestroy() {
        System.out.println("@PreDestroy: Cleanup logic before bean is removed from container.");
    }

    @Override
    public void destroy() {
        System.out.println("destroy(): Called during bean destruction.");
    }
}
package com.example.lifecycle;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;

@SpringBootApplication
public class SpringBeanLifeCycleApplication {

    public static void main(String[] args) {
        ConfigurableApplicationContext context = SpringApplication.run(SpringBeanLifeCycleApplication.class, args);

        // Trigger bean to initialize
        LifeCycleBean bean = context.getBean(LifeCycleBean.class);

        // Close context to see destroy behavior
        context.close();
    }
}
