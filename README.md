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






package com.docsconsole.spring5.lifecycle.xml.awareinterfaces;

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

package com.docsconsole.spring5.lifecycle.xml.awareinterfaces;

import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class MainAppClient {
    public static void main(String[] args) {

        ConfigurableApplicationContext context = new ClassPathXmlApplicationContext("spring-beans1.xml");
        ASpringBean1 aSpringBean1 = context.getBean(ASpringBean1.class);
        context.close();

    }
}


<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns="http://www.springframework.org/schema/beans"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="aSpringBean" class="com.docsconsole.spring5.lifecycle.xml.callbackinterfaces.ASpringBean"></bean>

</beans>


package com.docsconsole.spring5.lifecycle.xml.callbackinterfaces;

import org.springframework.beans.factory.DisposableBean;
import org.springframework.beans.factory.InitializingBean;


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



package com.docsconsole.spring5.lifecycle.xml.callbackinterfaces;


import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

class MainAppClient {
    public static void main(String[] args) {

        ConfigurableApplicationContext context = new ClassPathXmlApplicationContext("spring-beans.xml");
        ASpringBean aSpringBean = context.getBean(ASpringBean.class);
        context.close();


    }
}



<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns="http://www.springframework.org/schema/beans"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="aSpringBean1" class="com.docsconsole.spring5.lifecycle.xml.awareinterfaces.ASpringBean1"></bean>

</beans>


package com.docsconsole.spring5.lifecycle.xml.initdestroy;

public class ASpringBean2 {
    public void customInit() {
        System.out.println("ASpringBean2:::--->@@customInit");
    }

    public void customDestroy() {
        System.out.println("ASpringBean2:::--->@@customDestroy()");
    }
}




package com.docsconsole.spring5.lifecycle.xml.initdestroy;


import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class MainAppClient {
    public static void main(String[] args) {

        ConfigurableApplicationContext context = new ClassPathXmlApplicationContext("spring-beans2.xml");
        ASpringBean2 aSpringBean2 = context.getBean(ASpringBean2.class);
        context.close();


    }
}





<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns="http://www.springframework.org/schema/beans"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="aSpringBean2" init-method="customInit" destroy-method="customDestroy"
          class="com.docsconsole.spring5.lifecycle.xml.initdestroy.ASpringBean2"></bean>

</beans>




package com.docsconsole.spring5.lifecycle.xml.postconstructpredestroy;

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





package com.docsconsole.spring5.lifecycle.xml.postconstructpredestroy;

import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class MainAppClient {
    public static void main(String[] args) {

        ConfigurableApplicationContext context = new ClassPathXmlApplicationContext("spring-beans3.xml");
        ASpringBean3 aSpringBean3 = context.getBean(ASpringBean3.class);
        context.close();

    }
}


<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns="http://www.springframework.org/schema/beans"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="aSpringBean3" class="com.docsconsole.spring5.lifecycle.xml.postconstructpredestroy.ASpringBean3"></bean>

</beans>






C:\USERS\D951857\WORKSPACE\SPRING-BEAN-LIFE-CYCLE-EXAMPLES
|   pom.xml
|   Spring-Bean-Life-Cycle-Examples.iml
|
+---.idea
|       compiler.xml
|       misc.xml
|       uiDesigner.xml
|       workspace.xml
|
+---src
|   +---main
|   |   +---java
|   |   |   \---com
|   |   |       \---docsconsole
|   |   |           \---spring5
|   |   |               \---lifecycle
|   |   |                   +---annotations
|   |   |                   |   +---awareinterfaces
|   |   |                   |   |       AppConfig.java
|   |   |                   |   |       ASpringBean1.java
|   |   |                   |   |       MainAppClient.java
|   |   |                   |   |
|   |   |                   |   +---callbackinterfaces
|   |   |                   |   |       AppConfig.java
|   |   |                   |   |       ASpringBean.java
|   |   |                   |   |       MainAppClient.java
|   |   |                   |   |
|   |   |                   |   +---initdestroy
|   |   |                   |   |       AppConfig.java
|   |   |                   |   |       ASpringBean2.java
|   |   |                   |   |       MainAppClient.java
|   |   |                   |   |
|   |   |                   |   \---postconstructpredestroy
|   |   |                   |           AppConfig.java
|   |   |                   |           ASpringBean3.java
|   |   |                   |           MainAppClient.java
|   |   |                   |
|   |   |                   \---xml
|   |   |                       +---awareinterfaces
|   |   |                       |       ASpringBean1.java
|   |   |                       |       MainAppClient.java
|   |   |                       |
|   |   |                       +---callbackinterfaces
|   |   |                       |       ASpringBean.java
|   |   |                       |       MainAppClient.java
|   |   |                       |
|   |   |                       +---initdestroy
|   |   |                       |       ASpringBean2.java
|   |   |                       |       MainAppClient.java
|   |   |                       |
|   |   |                       \---postconstructpredestroy
|   |   |                               ASpringBean3.java
|   |   |                               MainAppClient.java
|   |   |
|   |   \---resources
|   |           spring-beans.xml
|   |           spring-beans1.xml
|   |           spring-beans2.xml
|   |           spring-beans3.xml
|   |
|   \---test
|       \---java
\---target
    |   Spring-Bean-Life-Cycle-Examples-1.0-SNAPSHOT.jar
    |
    +---classes
    |   |   spring-beans.xml
    |   |   spring-beans1.xml
    |   |   spring-beans2.xml
    |   |   spring-beans3.xml
    |   |
    |   \---com
    |       \---docsconsole
    |           \---spring5
    |               \---lifecycle
    |                   +---annotations
    |                   |   +---awareinterfaces
    |                   |   |       AppConfig.class
    |                   |   |       ASpringBean1.class
    |                   |   |       MainAppClient.class
    |                   |   |
    |                   |   +---callbackinterfaces
    |                   |   |       AppConfig.class
    |                   |   |       ASpringBean.class
    |                   |   |       MainAppClient.class
    |                   |   |
    |                   |   +---initdestroy
    |                   |   |       AppConfig.class
    |                   |   |       ASpringBean2.class
    |                   |   |       MainAppClient.class
    |                   |   |
    |                   |   +---postconstructpredestroy
    |                   |   |       AppConfig.class
    |                   |   |       ASpringBean3.class
    |                   |   |       MainAppClient.class
    |                   |   |
    |                   |   \---xml
    |                   |       \---awareinterfaces
    |                   |               AppConfig.class
    |                   |               ASpringBean1.class
    |                   |               MainAppClient.class
    |                   |
    |                   \---xml
    |                       +---awareinterfaces
    |                       |       ASpringBean1.class
    |                       |       MainAppClient.class
    |                       |
    |                       +---callbackinterfaces
    |                       |       ASpringBean.class
    |                       |       MainAppClient.class
    |                       |
    |                       +---initdestroy
    |                       |       ASpringBean2.class
    |                       |       MainAppClient.class
    |                       |
    |                       \---postconstructpredestroy
    |                               ASpringBean3.class
    |                               MainAppClient.class
    |
    +---generated-sources
    |   \---annotations
    +---maven-archiver
    |       pom.properties
    |
    \---maven-status
        \---maven-compiler-plugin
            +---compile
            |   \---default-compile
            |           createdFiles.lst
            |           inputFiles.lst
            |
            \---testCompile
                \---default-testCompile
                        inputFiles.lst


```

