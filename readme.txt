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



