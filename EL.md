# EL

: Expression Language

- 기존의 jsp에서 사용한 <%= request.getParameter("key") %> 를  ${	} 의 형식으로 parameter의 정보를 쉽게 추출, 출력할 수 있다.



## EL 문자 

- 논리 : true, false

- 숫자 : 정수, 실수

- 문자열 : " ", ' '

  ```
  ${true}
  ${123}
  ${1.5}
  ${"el"}
  ${'el'}
  ```

## EL 연산자

- 산술 연산자 : +, -, /, *, %, mod

- 논리 연산자 : &&, ||, !, and, or, not

- 비교 연산자 : ==, !=, <, >, <=, >=, eq, ne, lt, get, le, ge

- empty 연산자 : null 또는 공백 체크

  ```
  ${empty "" }	->	true
  ${empty null}	->	true
  ```



## EL 예약어

: 이미 기능과 이름이 정의되어 있어서 변수로 사용할 수 없는 단어

- and, eq, or, instanceof, true, false 등등

req에 없으면, 자동으로 session, application으로 찾아가서 데이터의 이름과 값을 가져온다.

## EL 내장 객체

: 내부적으로 변수 선언과 초기화 작업이 자동으로 되어있어, 참조변수의 이름만 알아 이름으로 바로 접근하여 사용이 가능하다. 

- param : Query String의 이름과 값을 저장하고 있는 map 객체

  ​			 웹브라우저에서 전송된 질의 문자열 저장 객체

  ```
  in jsp
  <body>
  	${param.id}
  	${param["id"]}
  	<jsp:forward page="${param.p}"/>
      :	해당 jsp를 호출한 jsp 에서 <jsp:forward page="<%=p%>"/> 가 수행되어
     		"p"가 key인 데이터의 값을 화면에 출력
  </body>
  ```

  

- header : 요청 정보 헤더의 정보들을 이름과 값으로 저장하고 있는 map 객체

  ```
  ${header}
  ```

  

- requestScope : HttpServletRequest에 등록된 데이터의 이름과 값을 저장하고 있은 map 객체

- sessionScope : HttpSession에 등록된 데이터의 이름과 값을 저장하고 있은 map 객체

- cookie : 요청을 보낸 클라이언트의 쿠키 이름과 값을 저장하고 있은 map 객체

- applicationScope : ServletContext에 등록된 데이터의 이름과 값을 저장하고 있은 map 객체 

- ...



### booklist2 ==> EL 표현식으로 바꿈

- jsp 파일 상단에 "<%@ taglib prefix="c" uri="http://java.sun.com/jstl/core" %>"를 추가하여, jstl을 사용할 수 있도록 한다.

```
<%@ taglib prefix="c" uri="http://java.sun.com/jstl/core" %>

<body>
	<table>
 		<tr><th>No</th><th>이름</th><th>작가</th><th>가격</th><th>날짜</th></tr>			
 		<c:forEach var="book" items="${list}">
		<tr>
			<td>${book.bookno}</td>
			<td>${book.title}</td>
			<td>${book.author}</td>
			<td>${book.price}</td>
		</tr>		
		</c:forEach>

	</table>
</body>
```

### items="${list}"

- key값 "list"에서 가져온 값을 items으로 받아, 자동으로 request의 객체 안에 있는 데이터를 추출함

# JSP 태그로 화면 layout 분리 

- jsp 페이지는 xml기반의 페이지 ==> 태그를 무한으로 확장, 사용자 정의 태그
- html 문서를 jsp로 쪼개어, header, footer, nav 등을 효율적으로 관리하고 유지보수 한다. 

- 기본으로 지원하는 jsp태그

```
<jsp:include page="header.jsp"></jsp:include>   
```

### 





















































































