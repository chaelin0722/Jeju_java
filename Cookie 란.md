### Cookie 란?

<hr>

**웹에서 쿠키(Cookie)의 사용**



**1. 쿠키(Cookie)의 개요**



\- HTTP 프로토콜은 상태가 없다. 즉 이전에 무엇을 했고, 지금 무엇을 했는지에 대한 정보를 갖고 있지 않는 특성을 가지고 있다.

즉, 웹 브라우저(클라이언트)의 요청에 대한 응답을 하고 나면 해당 클라이언트와의 연결을 지속하지 않는다 (Connectionless)



\- HTTP 프로토콜은 상태에 대한 지속적인 연결이 없다. 따라서 이런 부분을 해결하기 위해서 웹 서버 측에 웹 브라우저의 정보를 저장한 후 계속되는 웹브라우저의 요청 속에 포함되어 있는 웹 브라우저의 정보와 비교해서 동일한 웹 브라우저로부터 온 요청을 판단할 수 있다.



\- 쿠키(Cookie)는 상태가 없는 프로토콜을 위해 상태를 지속시키기 위한 방법이다. 쿠키는 웹 브라우저의 정보를 웹 브라우저에 저장하므로, 이후에 서버로 전송되는 요청에는 쿠키가 가지고 있는 정보가 같이 포함돼 전송된다. 이때 웹 서버는 웹 브라우저의 요청 속에 포함되어 있을 쿠키를 읽어서 새로운 웹 브라우저인지 이전에 요청을 했던 웹 브라우저인지를 판단할 수 있다.



\- 이러한 방법으로 웹 브라우저를 통해서 특정 사이트에 접속하면 웹 브라우저에 쿠키가 저장되어 접속한 사용자의 정보가 유지되는 것이다.

 

![img](https://t1.daumcdn.net/cfile/tistory/2426894D526CC0D407)

\- 쿠키는 웹 사이트에 접속할 때 생성되는 정보를 담은 임시 파일이다. 일반적으로 쿠키는 4KB 이하의 크기로 생성된다. 이러한 쿠키의 목적은 원래 사이트에 접속한 사용자의 정보를 유지하거나, 사이트에 접속하는 사용자들이 해당 사이트에 쉽게 접속하기 위한 것이다.



\- 어떤 웹 사이트를 처음 방문해서 로그인해 사용하고 나면, 아이디와 패스워드를 기록한 쿠키가 만들어진다. 그 다음부터 해당 사이트에 접속하면 별도의 절차 없이 사이트에 빠르게 연결할 수 있게 된다. 쿠키는 이러한 목적으로 사용하기 위해 만들어진 것이다.



\- 그러나 쿠키는 웹 브라우저가 방문했던 웹 사이트에 대한 정보 및 개인의 정보가 기록되기 때문에 개인의 사생활이나 정보를 침해할 소지가 있다는 문제점을 안고 있다. 이러한 보안상의 문제를 조금이나마 해소하기 위해서 웹 브라우저 자체에 쿠키 거부 기능이 추가되었다.



\- 쿠키에 대한 거부가 웹 브라우저에 설정되어 있으면, 쿠키 본래의 목적인 웹 브라우저와의 연결을 지속시키는 기능을 수행할 수 없게 된다. 따라서 이것은 쿠키의 가장 치명적인 단점이 된다.



**2. 쿠키(Cookie)의 사용**



\- JSP에서 쿠키를 사용하려면 javax.servlet.http 패키지에 있는 Cookie 클래스의 객체를 생성해야 한다. 이렇게 생성된 쿠키에는 각각의 웹 브라우저를 판별할 수 있는 정보가 포함되어 있다. 쿠키는 웹 서버가 웹 브라우저의 요청에 응답할 때 response 객체에 실려서 사용자의 웹 브라우저에 저장된다.



\- 웹 브라우저에 저장된 쿠키는 사용자가 다시 웹 서버에 요청을 할 때 request 객체에 실려서 다시 웹 서버에 전달된다. 이때 웹 서버는 전달된 쿠키의 값을 읽어서 같은 웹 브라우저로부터 온 요청인지를 판별하게 된다.



\- 이러한 방법에 의해 웹 서버는 각각의 웹 브라우저와의 상태를 지속시킬 수 있는 것이다.



**3. 쿠키 생성 및 사용**



\- 쿠키는 이름, 값, 유효기간, 도메인, 경로 등으로 이루어져 있다. 이들 중 가장 중요한 구성 요소는 쿠키의 이름과 값이다.



**(1) 쿠키 생성하기**



<%

Cookie info = new Cookie("testCookie", "Hello Cookie");    // 쿠키를 생성한다. 이름:testCookie, 값 : Hello Cookie



info.setMaxAge(365*24*60*60);                                 // 쿠키의 유효기간을 365일로 설정한다.

info.setPath("/");                                                    // 쿠키의 유효한 디렉토리를 "/" 로 설정한다.

response.addCooke(info);                                    // 클라이언트 응답에 쿠키를 추가한다.

%>



**(2) 쿠키에 저장된 정보 읽어오기**

<%

Cookie[] cookies = request.getCookies();            // 요청정보로부터 쿠키를 가져온다.

out.println("현재 설정된 쿠키의 개수 : " + cookies.length);    // 쿠키가 저장된 배열의 길이를 가져온다.



for(int i = 0 ; i<cookies.length; i++){                            // 쿠키 배열을 반복문으로 돌린다.



out.println(i + "번째 쿠키 이름 : " + cookies[i].getName());            // 쿠키의 이름을 가져온다.

out.println(i + "번째 쿠키에 설정된 값 : " + cookies[i].getValue());    // 쿠키의 값을 가져온다

}

%>



**(3) 설정된 쿠키를 모두 삭제하기**

<%

Cookie[] cookies = request.getCookies();            // 요청정보로부터 쿠키를 가져온다.



for(int i = 0 ; i<cookies.length; i++){                            // 쿠키 배열을 반복문으로 돌린다.



cookies[i].setMaxAge(0);                        // 특정 쿠키를 더 이상 사용하지 못하게 하기 위해서는 

// 쿠키의 유효시간을 만료시킨다.

response.addCookie(cookies[i]);            // 해당 쿠키를 응답에 추가(수정)한다.

}

%>



**4. 쿠키 관련 메소드**

| 메소드                  | 설명                                               |
| ----------------------- | -------------------------------------------------- |
| String getCommnet()     | 쿠키에 대한 설명을 가져온다.                       |
| String getDomain()      | 쿠키의 유효한 도메인 정보를 가져온다.              |
| int getMaxAge()         | 쿠키의 사용할 수 있는 기간에 대한 정보를 가져온다. |
| String getName()        | 쿠키의 이름을 가져온다                             |
| String getPath()        | 쿠키의 유효한 디렉토리 정보를 가져온다.            |
| boolean getSecure()     | 쿠키의 보안이 어떻게 설정되어 있는지 가져온다.     |
| String getValue()       | 쿠키에 설정된 값을 가져온다.                       |
| int getVersion()        | 쿠키의 버전을 가져온다.                            |
| void setComment(String) | 쿠키에 대한 설명을 설정한다.                       |
| void setDomain(String)  | 쿠키에 유효한 도메인을 설정한다.                   |
| void setMaxAge(int)     | 쿠키의 유효한 기간을 설정한다.                     |
| void setPath(Striong)   | 쿠키의 유효한 디렉토리를 설정한다.                 |
| void setSecure(boolean) | 쿠키의 보안을 설정한다.                            |
| void setValue(String)   | 쿠키의 값을 설정한다.                              |
| void setVersion(int)    | 쿠키의 버전을 설정한다.                            |









**5. 쿠키 사용 예제**



**(1) 쿠키 읽어서 가져오기    (자동 로그인 처리)**



<%@ page language ="java" contentType ="text/html;charset=EUC-KR" pageEncoding="EUC-KR"%>



<%

String id = "";



try{

Cookie[] cookies = request.getCookies();                 // 요청에서 쿠키를 가져온다.



if(cookies!=null){                                                    // 쿠키가 Null이 아닐때,



for(int i=0; i<cookies.length; i++){                        // 쿠키를 반복문으로 돌린다.

if(cookies[i].getName().equals("id")){            // 쿠키의 이름이 id 일때

id=cookies[i].getValue();                        // 해당 쿠키의 값을 id 변수에 저장한다.

}

}

if(id.equals("")){                                            // 쿠키에서 이름 id를 찾지 못했을때

response.sendRedirect("loginForm.jsp");    // loginForm 으로 리다이렉트 한다.

}



}else{                                                                // 요청에서 쿠키가 없을때

response.sendRedirect("loginForm.jsp");    // loginForm 으로 리다이렉트 한다.

}

}catch(Exception e){}

%>



**(2) 쿠키 저장하기    (로그인 정보 등록)**



<%@ page language ="java" contentType ="text/html;charset=EUC-KR" pageEncoding="EUC-KR"%>

<% request.setCharacterEncoding("euc-kr"); %>



<%

String id = request.getParameter("id");                        // 요청에서 id 값을 가져온다.

String passwd = request.getParameter("passwd");      // 요청에서 passwd 값을 가져온다.



.....                                                // id 와 passwd 로 로그인 을 확인한다.



if(check == 1){                                // 로그인이 성공일때,



Cookie cookie = new Cookie("id", id);        // id 라는 이름과 request의 id 값으로 쿠키 생성

cookie.setMaxAge(20*60);                        // 쿠키의 유효시간을 20분으로 설정

response.addCookie(cookie);                    // 쿠키를 응답에 추가

response.sendRedirect("cookieMain.jsp");    // cookieMain 으로 리다이렉트



}else {}



%>



**(3) 쿠키 삭제하기    (로그아웃)**



<%@ page language ="java" contentType ="text/html;charset=EUC-KR" pageEncoding="EUC-KR"%>



<%

Cookie[] cookies = request.getCookies();                    // 요청에서 쿠키를 가져온다.



if(cookies!=null){                                            // 쿠키가 Null이 아니라면



for(int i=0; i<cookies.length; i++){                // 쿠키를 반복문으로 돌린다.



if(cookies[i].getName().equals("id")){        // 쿠키의 이름이 id 일때

cookies[i].setMaxAge(0);                    // 쿠키의 유효시간을 0 으로 셋팅한다.

response.addCookie(cookies[i]);        // 수정한 쿠키를 응답에 추가(수정) 한다.

}}}

&>