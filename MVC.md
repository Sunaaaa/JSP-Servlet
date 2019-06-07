

# MVC design pattern

: 업무 로직과 화면(UI) 담당을 분리한다.

- servlet : 프로세스, 비즈니스 로직	=> html 태그 절대  넣지 않는다.
- jsp : 화면 구성 	=> 자바 코드 절대 넣지 않는다.



- Model, View, Controller를 명확하게 분리하여 작업 한다.

  - Model : 자바 빈즈(java beans)
  - View : html, jsp
  - Controller : servlet
  - 데이터 access layer(DAO), 데이터를 외부로 노출시키는 service layer 등 layer를 분리한다.

  

- dispatcher 

  : servlet으로 들어온 요청 흐름(제어권)을 jsp 로 넘겨준다.

  - forward : 호출한 페이지로 흐름이 아예 가버린다.	

    =>	필요한 데이터를 request 객체에 담고, 호출된 jsp("/booklist2.jsp")에서 request 객체에서 데이터를 꺼낸 뒤 출력한다.

    ```
    getServletContext().getRequestDispatcher("/booklist2.jsp")
    .forward(request, response);
    ```

    

  - including : 요청 흐름이 호출한 페이지로 갔다가 다시 되돌아온다.

  

- redirect 

  - a.jsp 에서 response.sendRedirect("b.jsp")를 호출하면, 각각의 jsp가 Clinet와 요청/응답한다. 

    - Clinet --request--> a.jsp --response--> Clinet --request--> b.jsp --response-> Clinet

  - request 객체가 공유되지 않는다. 

    ```
    response.sendRedirect("ListBookService");
    ```

    

- servlet에서 jsp 로 포워딩 하기

  - servlet이 추출한 결과값을 jsp가 받아 원하는 형태로 화면에 데이터를 출력한다. 

  - request를 통하여 servlet과 jsp 사이의 데이터를 교환할 수 있다.

    ==> request는 servlet과 jsp의 공유 데이터 이다.

p248



## Model 1 아키텍처

:  jsp가 아닌 서비스 layer에서 DB와 연동한다.

	- 서비스 layer : jsp가 담당하던 business logic과 data access logic을 전담한다. 
	- jsp : Clinet의 request를 분석하고 응답한다.

: jsp 입장에선 서비스 layer는 workBean(DAO, sevice, VO...)으로 business logic을 담당하고 재사용성과 유지보수성을 향상시킨다.



*** jsp 에서 직접 DB연동하는 것은 Model1구조 조차 아님

*** jsp에 절대로 DB연동하는 코드를 삽입하지 않는다. 반드시 분리하자.

*** 실습 booklist3가 model1이다.



## Model 2 아키텍처

: jsp, servlet, ui가 모두 분리된다.

: 각각의 jsp, servlet, ui에는 DB와 연동하는 코드는 없다. 별도의 service interface를 통하여 상황별 DAO를 만들고,  DB와 연동하는 코드를 작성한다.

: 코딩과 유지보수가 쉽다.

*** 실습 booklist4, ListBookServlet, index.jsp가 model2이다.



### 실습

### =====

### 서블렛

### ListBookService : 데이터를 추출함, servlet에서 request에 list를 담아줌

request.setAttribute("list", list);

: servlet에서 request에 list를 담아줌

getServletContext().getRequestDispatcher("/booklist2.jsp").forward(request, response);

: forward 방식으로 jsp 호출

- servlet에서 에러 발생 시, 기존에 작성한 error.jsp로 이동하여 에러 화면 출력

  - ```
    } catch (Exception e) {
      			request.setAttribute("exception", e);
      			getServletContext().getRequestDispatcher("/error.jsp").forward(request, response);
      		}
    ```

  - ![1559714996830](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1559714996830.png)

    ​	*** 에러가 발생할 수  있는 모든 경우는 try{}catch{}로 묶기

### JSP

list를 화면에 출력하는 jsp 

스프링 교제 p241

## 