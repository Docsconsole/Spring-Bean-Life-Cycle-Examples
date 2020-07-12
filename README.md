# Spring-Bean-Life-Cycle-Examples
Set of examples for Spring-Bean-Life-Cycle-Examples


```
package com.docsconsole.spring5.lifecycle.annotations.awareinterfaces;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(basePackages = "com.docsconsole.spring5.lifecycle.annotations.awareinterfaces")
public class AppConfig {


}



package com.docsconsole.spring5.lifecycle.annotations.awareinterfaces;

import org.springframework.beans.BeansException;
import org.springframework.beans.factory.BeanClassLoaderAware;
import org.springframework.beans.factory.BeanFactory;
import org.springframework.beans.factory.BeanFactoryAware;
import org.springframework.beans.factory.BeanNameAware;
import org.springframework.context.*;
import org.springframework.context.weaving.LoadTimeWeaverAware;
import org.springframework.core.io.ResourceLoader;
import org.springframework.instrument.classloading.LoadTimeWeaver;
import org.springframework.jmx.export.notification.NotificationPublisher;
import org.springframework.jmx.export.notification.NotificationPublisherAware;
import org.springframework.stereotype.Component;

@Component
public class ASpringBean1 implements ApplicationContextAware,
        ApplicationEventPublisherAware, BeanClassLoaderAware, BeanFactoryAware,
        BeanNameAware, LoadTimeWeaverAware, MessageSourceAware,
        NotificationPublisherAware, ResourceLoaderAware {
    @Override
    public void setResourceLoader(ResourceLoader arg0) {
        // TODO Auto-generated method stub
        System.out.println("ASpringBean1:::--->@setResourceLoader");
    }

    @Override
    public void setNotificationPublisher(NotificationPublisher arg0) {
        // TODO Auto-generated method stub
        System.out.println("ASpringBean1:::--->@@setNotificationPublisher");

    }

    @Override
    public void setMessageSource(MessageSource arg0) {
        // TODO Auto-generated method stub
        System.out.println("ASpringBean1:::--->@@setMessageSource");
    }

    @Override
    public void setLoadTimeWeaver(LoadTimeWeaver arg0) {
        // TODO Auto-generated method stub
        System.out.println("ASpringBean1:::--->@@setLoadTimeWeaver");
    }

    @Override
    public void setBeanName(String arg0) {
        // TODO Auto-generated method stub
        System.out.println("ASpringBean1:::--->@@setBeanName");
    }

    @Override
    public void setBeanFactory(BeanFactory arg0) throws BeansException {
        // TODO Auto-generated method stub
        System.out.println("ASpringBean1:::--->@@setBeanFactory");
    }

    @Override
    public void setBeanClassLoader(ClassLoader arg0) {
        // TODO Auto-generated method stub
        System.out.println("ASpringBean1:::--->@@setBeanClassLoader");
    }

    @Override
    public void setApplicationEventPublisher(ApplicationEventPublisher arg0) {
        // TODO Auto-generated method stub
        System.out.println("ASpringBean1:::--->@@setApplicationEventPublisher");
    }

    @Override
    public void setApplicationContext(ApplicationContext arg0)
            throws BeansException {
        // TODO Auto-generated method stub
        System.out.println("ASpringBean1:::--->@@setApplicationContext");
    }
}



package com.docsconsole.spring5.lifecycle.annotations.awareinterfaces;

import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class MainAppClient {
    public static void main(String[] args) {

        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        ASpringBean1 aSpringBean1 = context.getBean(ASpringBean1.class);
        context.close();

    }
}




package com.docsconsole.spring5.lifecycle.annotations.callbackinterfaces;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(basePackages = "com.docsconsole.spring5.lifecycle.annotations.callbackinterfaces")
public class AppConfig {

}




package com.docsconsole.spring5.lifecycle.annotations.callbackinterfaces;

import org.springframework.beans.factory.DisposableBean;
import org.springframework.beans.factory.InitializingBean;
import org.springframework.stereotype.Component;


@Component
public class ASpringBean implements InitializingBean, DisposableBean {

    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("ASpringBean:::--->@afterPropertiesSet");
    }

    @Override
    public void destroy() throws Exception {
        System.out.println("ASpringBean:::--->@destroy");
    }
}




package com.docsconsole.spring5.lifecycle.annotations.callbackinterfaces;


import com.docsconsole.spring5.lifecycle.annotations.awareinterfaces.AppConfig;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

class MainAppClient {
    public static void main(String[] args) {

        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        ASpringBean aSpringBean = context.getBean(ASpringBean.class);
        context.close();

    }
}





package com.docsconsole.spring5.lifecycle.annotations.initdestroy;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(basePackages = "com.docsconsole.spring5.lifecycle.annotations.initdestroy")
public class AppConfig {

    @Bean(initMethod = "customInit", destroyMethod = "customDestroy")
    public ASpringBean2 aSpringBean2() {
        return new ASpringBean2();
    }

}





package com.docsconsole.spring5.lifecycle.annotations.initdestroy;

public class ASpringBean2 {
    public void customInit() {
        System.out.println("ASpringBean2:::--->@@customInit");
    }

    public void customDestroy() {
        System.out.println("ASpringBean2:::--->@@customDestroy()");
    }
}






package com.docsconsole.spring5.lifecycle.annotations.initdestroy;


import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class MainAppClient {
    public static void main(String[] args) {

        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        ASpringBean2 aSpringBean2 = context.getBean(ASpringBean2.class);
        context.close();

    }
}








package com.docsconsole.spring5.lifecycle.annotations.postconstructpredestroy;


import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(basePackages = "com.docsconsole.spring5.lifecycle.annotations.postconstructpredestroy")
public class AppConfig {
}




package com.docsconsole.spring5.lifecycle.annotations.postconstructpredestroy;

import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;

public class ASpringBean3 {

    @PostConstruct
    public void customInit() {
        System.out.println("ASpringBean3:::--->@@ostConstruct");
    }

    @PreDestroy
    public void customDestroy() {
        System.out.println("ASpringBean3:::--->@@preDestroy");
    }
}





package com.docsconsole.spring5.lifecycle.annotations.postconstructpredestroy;

import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class MainAppClient {
    public static void main(String[] args) {

        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        ASpringBean3 aSpringBean3 = context.getBean(ASpringBean3.class);
        context.close();

    }
}


```

