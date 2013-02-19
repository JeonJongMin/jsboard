start 게시판 제작 시작 2013.02.06





--------------------------------------------------------



2013.02.07 목요일

1) 게시판 구현 기획안 작성
2) database , table (count integer primary key autoincrement ,id text,subject text,message text) 생성
3) 댓글 기능은 제외, 게시판 글의 insert, delete, update 함수 구현




--------------------------------------------------------




2013.02.12 화요일


html : board_ver0212.html


1 댓글 기능 추가
- 기존의 게시판 글 목록에 댓글 셀을 추가하여 댓글을 구현함
- 데이터베이스의 테이블에 새로운 속성 super integer 를 추가하였다.
- super integer 는 댓글에만 값이 입력되는 속성으로서(댓글이 아닌경우 NULL) 댓글이 가리키는 글의 primary key를 나타낸다.
- 내용이 길어지면 표가 계속 커지는 현상을 방지하기 위해 스크롤 바 기능을 추가하였다.


2 게시판 작동 과정

1) 웹브라우저 실행
- 브라우저 실행 시 createDB() , createTable() 이 호출되어 DB와 Table이 없는 경우 새로 생성하고 있다면 기존의 데이터를 사용한다.
- 테이블의 속성값 : count integer primary key autoincrement ,id text,subject text,message text,super integer
- 브라우저 실행 시 selectDataAll() 함수가 호출된다. 이 함수는 DB에 저장된 게시판 데이터들을 웹에 표 형태로 보여주는 역할을 한다.
  게시판 표중 댓글 내용이 작성되는 셀에 댓글 표가 작성되며 selectReplyAll(count) 함수를 호출한다.
- selectReplyAll 함수는 primary key 를 매개변수로 받아 전체 데이터베이스 자료를 for문을 돌면서 super 의 키값이 매개변수와 같은값일때
  해당 댓글에 대한 표를 출력하는 함수이다.

2) 새글 등록
- 글 입력창에 제목 아이디 내용을 입력한 후 글 등록을 클릭하면 insertData() 함수가 호출되어 DB에 데이터가 저장된다.
- 저장후에 바로 사용자에게 보여주기 위해 새로고침기능인 myRefresh()함수를 호출하여 1)이 실행되도록 한다.

3) 글 삭제
- 삭제하고 싶은 글에 글 삭제 버튼을 누르면 deleteData(count) 함수가 호출되어 primary key를 매개변수로 받아와 테이블의 count와 값이 같거나
  super 와 값이 같은 경우 DELETE FROM 쿼리문을 실행한다.
- myRefresh() 함수를 호출한다.

4) 글 수정
- 글 입력창에 제목 아이디 내용을 입력한 후 글 수정을 클릭하면 updateData(count)함수가 호출된다.
  이 함수는 primary key 를 매개변수로 받아와 매개변수값과 같은 count를 갖는 레코드에 UPDATE 쿼리문 실행한다.
- myRefresh() 함수를 호출한다.

5) 댓글
- 댓글의 경우 insertReply 시에 추가적으로 super 값을 댓글이 가리키는 글의 primary key로 설정한다는 차이만 있을 뿐 나머지 기능은 위와 같다.




------------------------------------------------------------



2013.02.13 수요일


html : board_ver0213.html


1. 레코드 속성에 비밀번호 추가
1) create table Test (count integer primary key autoincrement ,id text,subject text,message text,password text,super integer)
2) input type="password" 를 생성하여 비밀번호를 입력받게 하였다.
3) insert후 deleteData나 updateData 함수 실행 시에 레코드의 password를 추가적으로 매개변수로 입력받아 사용자가 입력창에 입력한 password와 일치시에 함수를 실행하도록 하였다.


2. 표
1) 입력창과 게시판을 가운데정렬
2) 표를 좀더 보기 편하게 정리하였다.




------------------------------------------------------------


2013.02.14 목요일


html : board_ver0214.html


1. 레코드 속성에 작성 날짜 추가
1) create table Test (count integer primary key autoincrement ,id text,subject text,message text,date text,password text,super integer)

2. jQuery
1) 스크립트 toggle 함수 구현
2) toggle 함수를 이용하여 게시판의 내용과 댓글을 본문 확인 버튼을 이용하여 toggle 할 수 있도록 디자인하였다.
3) hide 기능을 이용해 글 입력창을 숨겨진 상태로 초기화하였다.



-------------------------------------------------------------




2013.02.15 금요일


html : board_ver0215.html


1. 게시판 화면구성
1) 전반적으로 게시판 화면 구성을 좀더 보기 편하게 다시 리모델링하여 구현하였다.
2) 작성일을 제목이 있는 행으로 위치를 변경하였다.
3) 댓글을 본 글 오른쪽에서 아래로 위치를 변경하였다.
4) 게시글마다 구분이 가기 쉽게 테두리에 색, 굵기등을 변경하였다.
5) 글의 내용과 댓글을 본문확인 버튼을 통하여 toggle 되도록 구현하였다.
6) 배경 색을 지정하였다.


2. 버튼 UI 변경
1) <Style> 을 이용하여 버튼의 UI를 변경하였다.




--------------------------------------------------------------




2013.02.18 화요일


html : board_ver0218.html

게시판 페이징 구현 버전.


1. 게시판 페이징 개요
1) 한 페이지당 5개의 글을 보여준다.
2) 화면 하단에 페이지 링크들을 표시한다. 자체 페이지링크 수는 최대 5 (ex 이전 1 2 3 4 5 다음) 이다.
3) 첫 페이지의 경우 이전페이지 링크는 생략. 마지막 페이지의 경우 다음페이지 링크는 생략한다.
4) 페이지 표시 예 : 첫 페이지  이전 페이지  6 7 8 9 10  다음페이지  끝 페이지


2. 페이징 구현 (getPageCount(StartPoint))
1) 현재 페이지 넘버를 표시하는 전역변수 globalpage를 선언.
2) 페이징 출력 함수 getPageCount(startPoint)
   - int 형 매개변수를 받아온다.(현재 페이지 넘버 받아옴)
   - 매개변수를 5로나눈 나머지 값을 얻는다.
   - db에 저장된 개시글의 개수를 받아와 5로 나누어 페이지의 전체 개수를 구한다.
   - startPoint와 위에서 구한 변수들을 이용하여 globalpage를 기준으로 5개의 페이지 링크를 생성한다.
   - 재귀를 사용하여 이전페이지, 다음페이지를 구현한다.
   - getPageCount(0) : 처음 페이지 ,  getPageCount(max-1) : 끝 페이지









---------------------------------------------------------------