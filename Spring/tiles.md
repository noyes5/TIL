# Tiles Framework
> tile이라는 이름 그대로 페이지를 조각으로 나누어 하나의 페이지에 조립해서 사용할 수 있게 도와주는 프레임워크

-----
## 예시 코드
mainTemplate.jsp
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%@ taglib prefix="tiles" uri="http://tiles.apache.org/tags-tiles" %>
<!DOCTYPE html>
<html>
  <!-- 헤드영역 생략-->
<body>
	<!-- top영역 -->
	<tiles:insertAttribute name="top"></tiles:insertAttribute>
	<div class="container-fluid">
		<div class="row">
			<div class="col-lg-2 sidenav">
				<!-- 왼쪽 sub메뉴 -->
				<tiles:insertAttribute name="menu"></tiles:insertAttribute>
			</div>
			<div class="col-lg-10">
				<!-- 실제 작업할때마다 보여지는 교체될 작업페이지 -->
				<tiles:insertAttribute name="content"></tiles:insertAttribute>
			</div>
		</div>
	</div>
</body>
</html>
```
main-tiles.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE tiles-definitions PUBLIC
       "-//Apache Software Foundation//DTD Tiles Configuration 3.0//EN"
       "http://tiles.apache.org/dtds/tiles-config_3_0.dtd">
<tiles-definitions>
	<definition name="indexTemplate" template="/WEB-INF/layout/index.jsp">
		<put-attribute name="top" value="/WEB-INF/include/top.jsp"/>
		<put-attribute name="content" value="/WEB-INF/include/mainContent.jsp"/>
	</definition>
	
	<definition name="mainTemplate" template="/WEB-INF/layout/mainLayout.jsp">
		<put-attribute name="top" value="/WEB-INF/include/top.jsp"/>
		<put-attribute name="menu" value="/WEB-INF/menu/pub_menu.jsp"/>
		<put-attribute name="content" value="/WEB-INF/emp/login.jsp"/>
	</definition>
	
	<definition name="index" extends="indexTemplate">
	</definition>
	<definition name="login" extends="mainTemplate">
	</definition>	
	
</tiles-definitions>
```
menu-tiles.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE tiles-definitions PUBLIC
       "-//Apache Software Foundation//DTD Tiles Configuration 3.0//EN"
       "http://tiles.apache.org/dtds/tiles-config_3_0.dtd">
<tiles-definitions>
	<definition name="menu/sales" extends="mainTemplate">
		<put-attribute name="menu" 
				value="/WEB-INF/menu/sales_menu.jsp"/>
		<put-attribute name="content"
				value="/WEB-INF/emp/mypage.jsp"/>
	</definition>
</tiles-definitions>
```

----

## 설명
1. pom.xml에 tiles 라이브러리를 추가해야한다.
```xml
<!-- tiles -->
<dependency>
    <groupId>org.apache.tiles</groupId>
    <artifactId>tiles-jsp</artifactId>
    <version>3.0.8</version>
</dependency>
<dependency>
    <groupId>org.apache.tiles</groupId>
    <artifactId>tiles-servlet</artifactId>
    <version>3.0.8</version>
</dependency>
```
<code class="notranslate">tiles-jsp, tiles-servlet, spirng 간의 버전 호환성 확인이 필요함.</code>

2. 예시 코드의 mainTemplate.jsp 와 같이 레이아웃을 만들 페이지에서 taglib을 사용하여 insertAttribute 한다. 

3. 예시 코드의 main-tiles.xml 과 같이 설정파일을 만들어서 레이아웃을 등록한다. 
<br>definition template 값이 출발지가 되는 페이지고, put-attribute value 값이 도달할 페이지다. 
<br>\<definition name=""> : 만들어진 타일즈 템플릿의 이름.
<br>\<put-attribute name=""> : 연결할 페이지의 이름
<br>이렇게 만든 definition name을 extends를 통해 다른 이름으로 지정하고 컨트롤러에서 사용이 가능하다.

IndexController.java
```java
@Controller
public class IndexController {
	@RequestMapping("/index.do")
	public String index() {
		return "index";
	}
```
<br>또한 **menu-tiles.xml 과 같이 extends 를 통해 다른 페이지도 쉽게 연결이 가능하다.**

 
4. spring-config.xml에 tiles 설정파일을 읽을수 있게 beans를 등록하고, 뷰를 만들수 있도록  ViewResolver도 등록한다.

spring-config.xml
```xml
<!--  1. tiles 설정파일을 등록 -->
	<beans:bean id="tilesConfigurer" class="org.springframework.web.servlet.view.tiles3.TilesConfigurer">
		<beans:property name="definitions">
			<beans:list>
				<beans:value>/WEB-INF/**/*-tiles.xml</beans:value>
			</beans:list>
		</beans:property>
	</beans:bean> 
	<!-- 2. tiles 기반으로 뷰를 만들 수 있도록 ViewResolver 등록 -->
	<beans:bean id="tilesViewResolver" class="org.springframework.web.servlet.view.UrlBasedViewResolver">
		<beans:property name="viewClass" value="org.springframework.web.servlet.view.tiles3.TilesView" />
		<beans:property name="order" value="1" />
	</beans:bean>
```


