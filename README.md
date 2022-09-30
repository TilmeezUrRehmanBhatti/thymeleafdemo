

**What is Thymeleaf?**

+ Thymeleaf is a Java templating engine
+ Commonly used to generate the HTML views for web apps
+ However, it is a general purpose templating engine
    + Can use Thymeleaf outside of web apps

**What is a Thymeleaf template?**

+ Can be an HTML page with some Thymeleaf expressions
+ Include dynamic content from Thymeleaf expressions

<img src="https://user-images.githubusercontent.com/80107049/193254363-a5a39ef0-678f-49eb-978b-93de91b0f239.png" width="500" />


**Where is the Thymeleaf template processed?**

+ In a web app, Thymeleaf is processed on the server
+ Result included in HTML returned to browser

<img src="https://user-images.githubusercontent.com/80107049/193254422-e599c775-692f-4d58-89f9-4cc05ecee6f8.png" width="500" />



**Thymeleaf vs JSP**

+ Thymeleaf is similar to JSP
    + Can be used fir web biew templates

+ One key difference
    + JSP can only be used in a web environment
    + Thymeleaf can be used in web OR non.web environments

**Thymeleaf Use Cases(non-web)**

+ Email Template
    + When student signs up for course then send welcome email

```HTML
Hi <<firstName>>,
Thanks for joining <<course>>!
```

+ CSV Template
    + Generate a monthly report as CVS then upload to Google drive
```HTML
Product,Quantity,Price,Total
...
...
```

+ PDF template
    + Generate a travel confirmation PDF then send bia email
```PDF
Flight: <<flightNum>>
Depart: <<departAirport>>
Arrive: <<arrivalAirport>>
```


**FAQ: What should we use JSP or Thymeleaf?**

+ Depends on our project requirements
+ If we only need web views we can go either way
+ If we need a general purpose template engine (non-web) use Thymeleaf


**Thymeleaf Demo**

Server time stamp

**Development Process**

1. Add Thymeleaf to Maven POM file
2. Develop Spring MVC Controller
3. Create Thymeleaf template

_Step 1:Add Thymeleaf to Maven pom fie_

```XML
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-thymleaf</artifactId>
</dependency>
```

_Step 2:Develop Spring MVC Controller_

File:DemoConroller.java
```JAVA
@Controller
public class DemoController {
  
  @GetMapping("/")
  public String sayHello(Model theModel) {
    
    theModel.addAttribute("theData", new jaa.util.Data());
    
    return "helloworld";
  }
}
```

**Where to place Thymeleaf template**

+ In Spring Boot, our Thymeleaf template file go in
    + **src/main/resources/templates**

+ For web apps, Thymeleaf templates have a **.html** extension

_Step 3:Create Thymeleaf template_

File:src/main/resources/templates/helloworld.html
```HTML
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
  <head>...</head>
  
  <body>
    <p th:text="Time on the server is ` + ${theDate}" />
  </body>
  
</html>
```

+ `xmlns:th="http://www.thymeleaf.org"` is to use Thymeleaf expressions
+ `th:text` Thymeleaf expression


**Additional Features**

+ Looping and conditionals
+ Css and JavaScript integration
+ Template layouts and fragments


**Using CSS with Thymleaf Templates**

+ We have the option of using
    + Local CSS files as part of our project
    + Referencing remote CSS files

**Development Process**

1. Create CSS file
2. Reference CSS in Thymeleaf template
3. Apply CSS style

_Step 1:Create CSS file_

+ Spring will look for static resources in the directory
    + **src/main/resources/static**

File:demo.css
```CSS
.funny {
  font-style: italic;
  color: green;
}
```

_Step 2:Reference CSS in Thymeleaf template_
File:helloworld.html
```HTML
<head>
  <title>Thymeleaf Demo</title>
  
  <!-- reference css file -->
  <link rel="stylesheet" th:href="@{/css/demo.css}"/>
  
</head>
```

+ @ symbol Reference context path of application(app root)

_Step 3:Apply CSS_

File:helloworld.html
```HTML
<head>
  <title>Thymeleaf Demo</title>
  
  <!-- reference css file -->
  <link rel="stylesheet" th:href="@{/css/demo.css}"/>
  
</head>

<body>
  <p th:text="'Time on the server is ' + ${theDate}" class="funny" />
</body>
```



**Other search directories**

+ Spring boot will search following directories for static resources:
    + **/src/main/resources**
    1. /META-INF/resources
    2. /resources
    3. /static
    4. /public
    + Search order: top-down


**3rd Party CSS Libraries - Bootstrap**

+ Local Installation
+ Download Bootstrap file(s) and add to **/static/css** directory

```HTML
<head>
  ... ...
  
  <!--- referece CSS file -->
  <link rel="stylesheet" th:href="@{/css/bootstrap.min.css}" />
  
</head>
```
+ Remote File

 ```HTML
<head>
  ... ...
  
  <!--- referece CSS file -->
  <link rel="stylesheet" 
        href="https://stackpath.bootstrpcdn.com/....." />
</head>
```
