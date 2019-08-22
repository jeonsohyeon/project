---
description: edwith 웹 프로그래밍 부스트코스 수강 내용 정리.
---

# JSP

## 서블릿

JAVA를 이용해 동적 웹 페이지를 만드는 프로그램. 응답 결과를 만들때 사용.

생명주기 init, service, destroy.

* init : 메모리에 없을 때 첫 실행
* service : 메모리에 존재하고 새로고침 했을 때 실행
* destroy : 영역을 벗어나는 경우

httpServlet의 service 메소드를 오버라이딩 하는 것\(ex. doGet, doPost 처럼.\)

브라우저가 요청하면 WAS에서 HttpServlet Request/Response 를 생성하고 이를 웹앱의 서블릿에서 실행하는데, 서블릿의 메소드 내용으로 오버라이딩 해서 실행한다. 다시 WAS를 통해 브라우저에 응답결과를 전송한다.

## JSP

jsp 파일이 하나의 서블릿\(java\) 파일로 변환되어 작동한다.

jsp를 실행하면 서블릿 소스가 생성되고 실행 된다. 때문에 jsp의 내용은 jspService\(\) 안에 들어가게 되므로 내장객체를 바로 사용할 수 있다.

```text
<% 스크립트릿(scriptlet) %> //주로 프로그래밍 로직을 기술.
<%! 선언문(declaration) %> //전역변수, 메소드 선언.
<%= 표현식(Expression) %> //화면에 응답, 출력할 내용 기술.

<%-- jsp 주석(java에서 변환하지 않음) -->
```

## 리다이렉트\(redirect\)

```text
<% response.sendRedirect("fileName.jsp") %>
```

http 프로토콜로 정해진 규칙. 서버가 클라이언트에게 302 코드로 응답하고, url 정보를 location header 값으로 전송한다. 클라이언트는 302 코드라면 서버에 재 요청을 한다.

서블릿이나 jsp 는 httpServletResponse 가 가지고 있는 sendRedirect\(\) 메소드를 사용한다.

{% hint style="danger" %}
포워드\(forward\)와의 차이점?

* 리다이렉트 : 요청/응답 객체가 2번 생성된다.
* 포워드 : 요청/응답 객체가 1번 생성된다.
{% endhint %}

## 포워드\(forward\)

서버 내부적으로 서블릿이 일부만 처리하고 다른 누군가에게\(다른 서블릿\) 일부를 처리하고 응답하게 함. 서블릿끼리의 지역변수를 공유하는 무언가가 필요하다. \(request.setAttribute 로 처리.\)

서블릿의 service\(\) 메소드 안에서

1. 보낼 값을 request.setAttribute\("변수명", 보낼 객체\)
2. RequestDispatcher 변수명 = Request.getRequestDispatcher\("전달할 서블릿 or jsp"\)
3. 변수명.forward\(request, response\);

전달받은 서블릿이나 jsp 에서 request.getAttribute\("변수명"\)으로 받는다.

{% hint style="info" %}
로직은 서블릿에서 수행하게 하고, 결과 출력은 jsp 에서 하는 것이 유리하다.
{% endhint %}

## 스코프\(Scope\)

### 페이지 스코프\(page scope\)

* pageContext 내장객체로 사용 가능
* forward 면 해당. page 스코프 변수는 사용 불가.
* 마치 지역 변수처럼 사용된다.

### 리퀘스트 스코프\(request scope\)

* request 내장객체 사용\(jsp\)
* httpServletRequest 객체 사용\(서블릿\)
* forward 시 값을 유지하고자 사용한다.

{% hint style="warning" %}
리다이렉트는 요청이 2번 발생되기 때문에 request 스코프를 벗어나게 된다.
{% endhint %}

### 세션 스코프\(session scope\)

* 브라우저 탭 끼리 세션 공유가 가능하다.
* httpSession 인터페이스를 이용한다.
* getSession\(\) 으로 세션객체를 얻는다.\(서블릿\)
* session 내장 변수를 이용한다.\(jsp\)
* 사용자 별로 유지되어야 할 정보가 있을 때 사용한다.

### 어플리케이션 스코프\(application scope\)

* 프로젝트 1개가 1개의 웹 어플리케이션이며, 하나의 서버에는 여러 앱이 있을 수 있다.
* 모든 클라이언트가 공통으로 사용해야 할 값이 있을 때 사용한다.

