###자바의 빈 설정 방법

자바 기반 설정 방식(Java-based configuration)
자바 클래스에 @Configuration 어노테이션을, 메서드에 @Bean 어노테이션을 사용해 빈을 정의 하는 방법으로 스프링 3.0.0부터 사용가능. 최근에는 스프링 기반 어플리케이션 개발에 자주 사용되고 특히 스프링 부트에서 이 방식을 많이 활용한다.

XML 기반 설정 방식(XML-based configuration)
XML파일을 사용하는 방법으로 <bean>요소의 class 속성에 FQCN(Fully-Qualified Class Name)을 기술하면 빈이 정의된다. <constructor-arg>나 <property> 요소를 사용해 의존성을 주입한다. 스프링 1.0.0부터 사용 가능.

어노테이션 기반 설정 방식(Annotation-based configuration)
@Controller 같은 마커 어노테이션(Marker Annotation)이 부여된 클래스를 탐색해서(Component Scan) DI 컨터이너에 빈을 자동으로 등록하는 방법이다. 스프링 2.5 부터 사용 가능.
