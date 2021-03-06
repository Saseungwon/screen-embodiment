# 🤾‍♀️ 화면구현 

## 📚 1일차
#### 👏 기본 개념 
- 프로토콜 → 통신규약
http = 웹서버

1. 웹서버 종류
   1. Apache : 모든 기능 다 가지고 있는 것
   2. NG2NX(엔진엑스) : Apache에 있는 기능 중 필요한 기능만 가져온 것
   3. Tomcat : 웹서버 + 자바
   4. IIS(Internet Information Server) : 윈도우 전용

2. proxy(대리) 서버
(1) forward proxy 서버	
```html
							        	a
									b
외부 실제 인터넷 	←         forward proxy 서버		  ←	c
									d
								 	e
```
- 장점
  -   사용자가 이용한 기록이  forward proxy에 캐쉬로 다 기록되어서 감시 가능
  - a가 사용한 것을 b가 이후에 사용할 때 캐쉬가 남아서 성능 높아짐

(2) backward proxy 서버
- 사용자 요청에 어느 서버로 가야하는지 알려주는 서버
```html
a							 이미지 서버
b							 검색 서버
c	 	→        backward proxy 서버      →   	 파일 서버
d						 	 …서버
e
```
#### 👏 설정하기
터미널에서
sudo service apache2 start  : 실행
http://127.0.0.1/ = http://localhost/
ps -ef | grep -i apache :  apache 가 실행중인지
sudo service apache2 stop : 중지 
sudo service apache2 restrart : 재시작
root / var / www/ html / index.html 에서  관리자 권한으로 텍스트편집기
- Apache2 Ubuntu default Page에서  default를 변경 가능
```html
 </style>
  </head>
  <body>
    <div class="main_page">
      <div class="page_header floating_element">
        <img src="/icons/ubuntu-logo.png" alt="Ubuntu Logo" class="floating_element"/>
        <span class="floating_element">
          Apache2 Ubuntu Saseungwon Page
```
 
- DNS 설정
  - etc/hosts/ hosts / 관리자권한으로 텍스트편집기
```html
127.0.0.1	localhost
192.168.20.87 kjh.net			// 설정 가능
127.0.1.1	pc42pc-B150M-DS3H

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```
- 사용하기 편하게 설정하기
  -   파일시스템 / etc /apache2 / sites-available / 000-default (사본).org /
```html
<VirtualHost *:80>
	# The ServerName directive sets the request scheme, hostname and port that
	# the server uses to identify itself. This is used when creating
	# redirection URLs. In the context of virtual hosts, the ServerName
	# specifies what hostname must appear in the request's Host: header to
	# match this virtual host. For the default virtual host (this file) this
	# value is not decisive as it is used as a last resort host regardless.
	# However, you must set it for any further virtual host explicitly.
	#ServerName www.example.com

	ServerAdmin webmaster@localhost
	DocumentRoot /var/www/html

	Alias /jsstudy /home/pc42-pc/jsstudy	// 설정 변경
```
  -   파일시스템 / etc /apache2 / apache2.conf /
```html
# Sets the default security model of the Apache2 HTTPD server. It does
# not allow access to the root filesystem outside of /usr/share and /var/www.
# The former is used by web applications packaged in Debian,
# the latter may be used for local directories served by the web server. If
# your system is serving content from a sub-directory in /srv you must allow
# access here, or in any related virtual host.
<Directory />
	Options Indexes FollowSymLinks	//권한설정
	AllowOverride ALL
	Require all granted
</Directory>

<Directory /usr/share>
	Options Indexes FollowSymLinks
	AllowOverride ALL
	Require all granted
</Directory>

<Directory /var/www/>
	Options Indexes FollowSymLinks
	AllowOverride ALL
	Require all granted
</Directory>

#<Directory /srv/>
#	Options Indexes FollowSymLinks
#	AllowOverride None
#	Require all granted
#</Directory>
```
- sudo service apache2 restart


#### 👏 기본 개념
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
</head>
<body>

<H1 style="color :yellow ;background-color: blue;"> 최고의 프로그래머"</H1>
<!-- 색 설정, 출력 -->
<input type=button value="누르시오"
style="width: 500px; height: 500px; font-size: 100px;"
onclick="f_click()">
<!-- 버튼 기능, 크기, 폰트크기 -->
<script>
function f_click(){
alert("눌렀습니다.")
}
</script>
<!-- 눌렀을 때 알람 -->
</body>
</html>

```

```html
<!-- 주석처리 컨트롤 슬러시(ctrl + /) -->
<!DOCTYPE html>
<!-- 기본 템플릿 : html : 5 -->
<!-- html 문서는 version5의 규칙을 따른다는 의미 -->
<html lang="en">
<!-- 검색엔진을 위해서 세팅해줌 "kr"로 쓰면 검색엔진이 한국인들에게 잘 보이게 됨 상황에 따라 세팅한다.-->
<head>
<!-- head : 메타(meta) 정보 -->
<meta charset="UTF-8">
<!-- 한글이 깨지면 'UTF-8' 을 빼먹어서 그럼 -->
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<!-- 기기 사이즈 화면에 비율을 맞춰줌 -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="shortcut icon" href="html.jpg" type="image/x-icon">
<!-- link : favicon - 파비콘 설정 -->
<title>제목을 남기세요</title>
<!-- 타이틀 이름 설정 -->
</head>
<body>
<!-- body 태그 안에 내용이 실제적으로 사용자에게 보이는 내용 -->
<h1>문자셋 UTF8 테스트</h1>
</body>
</html>
```

```html
<h1>이것만 써도 되나요?</h1>
<!-- h1 폰트가 가장 큼 -->
<meta charset="UTF-8">
<!-- <meta charset="UTF-8"> 만 써도 기본적으로 들어가야할 것들은 알아서 넣어줌 -->
<h2>써도된다.</h2>
<h3>써도된다.</h3>
<h4>써도된다.</h4>
<h5>써도된다.</h5>
<h6>써도된다.</h6>
<!-- h태그(header)는 6까지밖에 없다. -->
<h7>써도된다.</h7>
<h8>써도된다.</h8>
<!--
html은 엄격하지 않음. 이상한 게 있어도 알아서 처리해줌
기본적인 것이 빠지면 알아서 넣어준다.
-->

```
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
</head>
<body>
<!-- html이 나온 이유를 설명하는 태그 a
Hyper Text Markup(표시) Lauguage
-->
<!-- a태그 : 하이퍼텍스트 -->
<a href="http://daum.net">다음</a>
<!-- p태그 : 글이 단락으로 나눠짐. 개발자에겐 그닥 중요하진 않다. -->
<p>
그냥 글 단락(paragraph)을 표시하는 태그 p
</p>
<p>
p태그를 쓰면 글이 단락으로 나눠진다.
</p>

<!-- html에서는 엔터로 띄어지지 않는다. -->
안녕하세요.
프리태그입니다.

<!-- br 태그 : 엔터 기능-->
<br>안녕하세요.<br> br태그입니다.

<!-- &nbsp 태그 : 엔터 기능-->
<br>안녕하세요 &nbsp;&nbsp;&nbsp;&nbsp; nbsp태그입니다.

<!-- 특수키 : &lt; &gt; &copy; - 엔터(br)와 스페이스(nbsp) 빼고 다른 특수키들은 외우지 않아도 된다. -->
안녕하세요 &lt; &gt; &copy; 특수키 입니다.

<!-- pre 태그 : 쓴 대로 출력 -->
<pre>
여긴 그냥 쓴 대로 나온다.

쓴대로 보인다는 얘기다.
</pre>

<!-- ol 태그 : ordered list -->
<!-- li 태그 : list item : 앞에 숫자로 순차대로 정렬 -->
<ol>
<li>ssw</li>
<li>사승원</li>
<li>saseungwon</li>
</ol>

<!-- img 태그 : img ./ 파일에 있는 사진 삽입, alt: 대체문자열(요즘엔 거의 사용X) -->
<!--
src, width, height 등 태그 안에 정의하는 것을 속성(attribute)이라고 함
속성은 단위를 안 써도 되지만, style에는 꼭 단위를 써야됨
객체 하나는 element라고 부름
인스턴스와 오브젝트의 차이?
사람 인간(의미는 같은데 느낌이 다름)
미국사람 미국인간
-->
<img src="./img/images (2).jpeg" alt="">
<br>
<img src="./img/다운로드 (1).png" style="width: 300px; height: 400px;">
<br>
<img src="./img/다운로드 (1).png" alt="" width = 300 height = 400>
<br>
<img src="./img/html.jpg" alt="이미지가 안 나올 때 글자가 나오도록 설정하는 alt">

</body>
</html>

```

## 📚2일차


#### 👏 사용자 입력태그
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>사용자 입력태그</title>
</head>
<body>
<input type="button" value="난 버튼이야"><br>
<input type="text" value="난 텍스트 박스야">
<input type="hidden" value="난 눈에 안 보이는 텍스트 박스야">
<!--
radio : 동그란 모양의 체크
name : 하나의 그룹으로 묶어 오직 하나만 체크가 가능하게 된다.
checked : 만약 여성 회원만 가입할 수 있는 페이지면 check로 미리 체크해놓을 수 있음
-->
남<input type="radio" name="sb" value="male" >
여<input type="radio" name="sb" value="female" checked> <br>

<!-- checkbox 버튼도 name으로 그룹을 묶을 수 있으며 다중 선택이 가능 -->
보유한 스킬을 체크하세요(여러 개 사용가능) <br>
자바<input type="checkbox" name="skill" value="java">
SQL<input type="checkbox" name="skill" value="sql">
HTML<input type="checkbox" name="skill" value="html">
CSS<input type="checkbox" name="skill" value="css"> <br>

<select>
<!-- option : 누르면 선택할 수 있는 줄(?)이 나온다. -->
<option value="who"> 누구 좋아하세요? </option>
<option value="jv"> java </option>
<option value="HT"> HTML </option>
<option value="SQ"> SQL </option>
<option value="CS"> CSS </option>
<!-- selected로 디폴트 값을 설정해놓을 수 있음 -->
<option value="SQ" selected> SQL </option>
</select> <br>
<!-- textarea : 여러 줄의 텍스트를 입력할 때. 사용 사이즈 조절 가능 -->
<textarea rows=20 cols=30 > 여러 줄 입력할 때 사용한다.</textarea> <br>

<!--
기능이 괜찮아도 브라우져마다 보이는 모습이 다른 컴포넌트는 잘 사용되지 않음
특히 상업적인 사이트에는 더욱 더
-->
<!-- 색 선택 -->
<input type="color" value=""> <br>
<!-- 날짜 선택 -->
<input type="date" value=""> <br>
<!-- 범위 선택 -->
<input type="range" value=""> <br>
<!-- 숫자 선택 -->
<input type="number" value="4"><br>
<!-- file : 파일 업로드 가능한 버튼 -->
<input type="file" value=""><br>

</body>
</html>

```

#### 👏 테이블

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>테이블은 개발자가 많이 사용한다</title>
</head>
<body>
<!--
tr : table row
td : table data
값은 꼭 td 태그 안에 넣어야 함(중요)
-->
<table>
<tr><td>이름</td><td>별명</td></tr>
<tr><td>사승원</td><td>4win1</td></tr>
<tr><td>승원</td><td>win1</td></tr>

<!-- border : 테이블에 태두리 그려줌 -->
<table border=2 width = 500 >
<tr><td>이름</td><td>별명</td></tr>
<tr><td>사승원</td><td>4win1</td></tr>
<tr><td>승원</td><td>win1</td></tr>
<tr><td><img src="./img/images.jpeg" width=300 height= 300></td></tr>
<!-- colspan : 테이블 셀 합치기 -->
<tr><td colspan="2"><img src="./img/images.jpeg" width=500 height= 300></td></tr>
<!-- rowspan : 아래 셀에 있는 값 차지하고 싶을 때 -->
<tr><td rowspan="2">사승원</td><td>4win1</td></tr>
<tr><td>win1</td></tr>
<!-- 모든 셀 차지하고 싶을 때 -->
<tr><td rowspan="2" colspan="2">사승원</td></tr>
<tr></tr>

</table>

<!-- 문제 -->
<table border="3">

<tr><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td></tr>
<tr><td>2</td><td rowspan="2" colspan="3"><img src="./img/images.jpeg" ></td><td rowspan="2" colspan="3"><img src="./img/images.jpeg" ></td><td>2</td></tr>
<tr><td>3</td><td>3</td></tr>
<tr><td>4</td><td colspan="6">HTML</td><td>4</td></tr>
<tr><td>5</td><td rowspan="2" colspan="6"><img src="./img/images (2).jpeg" ></td><td>E</td></tr>
<tr><td>6</td><td>F</td></tr>
<tr><td>7</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td></tr>

</table>

<!-- 브라우저 호완성 체크 해야됨 : https://caniuse.com/background-clip-text
연습 : https://www.w3schools.com/html/default.asp
-->
</body>
</html>

```


#### 👏 화면나눠보기


```html

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>화면을 수직 3분할</title>

<style>
div{
border: 1px solid black;
/* height: 33vh;(class로 해서 필요없어짐) 수직으로 할 땐 vh, 수평으로 할 땐 vw*/
}
/* 태그의 class 속성을 통한 스타일 주기 */
.cl_d{
height: 10vh;
}
.cl_b{
height: 80vh;
}
.cl_f{
height: 10vh;
}
.cl_ssw{
display: inline-block;
width: 32%;
height: 100%;
}
</style>
</head>
<body>
<div class="cl_d">머릿글</div>
<div class="cl_b">
<div class="cl_ssw">왼쪽</div>
<div class="cl_ssw">가운데</div>
<div class="cl_ssw">오른쪽</div>
</div>
<div class="cl_f">바닥글</div>

</body>
</html>

```


#### 👏 div


```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
<style>
/* 내부 스타일 style sheet 주석 */
/* 특징 태그에 스타일 주기 */
div {
/*border-width: 10px; /보더 두께*/
/*border-style: groove; 보더 스타일*/
/*border-color: violet; 보더 색깔*/
display: inline-block; /* 옆에 누가 오는 걸 허용하지 않음 */
width: 50px; /* vw : % , px : px */
border : 10px groove violet; /* 축약기법 */

}
img{
/* display: block; (이미지는 자동으로 inline-block), 사진 하나씩 엔터하고 싶으면 block으로*/
width: 100px;
height: 100px;
}

</style>
</head>
<body>
<img src="./img/images.jpeg" >
<img src="./img/images.jpeg" >
<img src="./img/images.jpeg" >
<img src="./img/images.jpeg" >
<img src="./img/images.jpeg" >
<img src="./img/images.jpeg" >
<img src="./img/images.jpeg" >
<img src="./img/images.jpeg" >
<img src="./img/images.jpeg" >
<img src="./img/images.jpeg" >
<img src="./img/images.jpeg" >

<!--
html 문서를 도배할 정도로 많이 쓰이는 div 태그
레이아웃을 구성할 때 많이 사용하지만 css와 잘 조합하면 기본태그 기능도
커버하기 때문에 거의 만능태그로 불린다.
-->

<!-- div(divide) : 화면 나누는 것 -->
<!-- <div style="border:5px solid blue; margin: 100px; padding: 50px;">사승원 원승사</div> -->

<!-- display 속성으로 옆에 누가 올 수 있는 것을 제어할 수 있다. -->
<div>4win1</div>
<div>>SaSW</div>
<div>saseungwon</div>

</body>
</html>

```

#### 👏 css 기본선택자

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>css기본선택자</title>

<style>
/* 많이 쓰이는 선택자 일단 몇개만 */
div,img,input{
display: inline-block;
background-color: pink;
color: black; /* 글자색 */
width: 100px;
height: 100px;
}
/* 클래스 접근 = . (주로 디자이너가 사용) */
.cl_aa {
color: blue;
font-size: 30px;
}

/* 아이디 접근 = # (주로 개발자가 사용, 페이지 내에서 아이디는 유일하기를 권장)*/
#id_bb{
color: brown;
background-color: chartreuse;
}
</style>

</head>
<body>
<div class="cl_aa">난 div1</div>
<div id="id_bb">난 div2</div>
<div>난 div3</div>
<img src="./img/images.jpeg" >
<input type="button" value="눌러보세요">
</body>
</html>

```


#### 👏 스크립트 시작


```html
<!DOCTYPE html>
<meta charset="utf-8">
<!--
script 태그가 나타나면 브라우져 안의 스크립트 엔진이 동작
우리가 배우는 버젼은 브라우져 호완성을 위해서 ES5버전 기준
-->
<script>
// 프로그램 배울 때 가장 먼저 배워야 할 것은?. 출력문.
console.log("콘솔.로그 : 출력문은 어디에 나올까");// 세미콜론 필수
document.write("<h1>도큐먼트.라이트 : 이건 화면에 나온다.<h1>"); //h1 태그로 크기 조절 가능
alert("이걸 가장 많이 사용한다.");// 메세지 창, 반복문 같은 경우에 메세지 창이 계속 나오기 때문에 console.log가 권장됨

//자바 스크립트 언어의 특징
//변수선언에 var를 붙이는 것이 코드 가독성에 유리 (안 붙여도 상관없음)
//자바스크립트는 자바만큼 엄격하지 않아서 일부는 에러없이 실행이 되지 않음
//자바스크립트는 동적언어 이퀄(=) 오른쪽의 값에 따라 자동으로 데이터 타입이 결정됨
"use strict" // 변수 사용에 엄격모드 적용, 아주 권장됨 맨 윗줄에 기술해야됨
var ssw = "사승원" ; // 변수 ssw에 사승원이라는 문자열을 담아라
alert(ssw);
var ssw = 3; //선언부를 먼저 해석해서 미리 준비해두는 것은 hoisting 이라고 부른다.
alert(ssw);
</script>

```

## 📚 3일차
#### 👏 데이터타입

```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>
//javascript 데이터 타입
"use strict" //맨 첫 줄에 써주면 좋다
var v_num //숫자(Number)형
//alert(typeof(v_num));
var v_str = '사승원' // 문자열(String)형 // 문자열 안에 따옴표 넣고싶을 때 '사"승"원', "사'승'원"
//alert(v_str);
var v_bool = true; //불린(boolean), true, false
var v_null = null; //null. 아직 초기화하지 않았다는 표시
var v_array = ["사승원", "오승원", "육승원", true, 222, ["배열안에", "배열삽입", "가능"]];
//배열(자바스크립트는 자바와 달리 제약사항이 없다. 편하다.)
alert(v_array[5][0]);
var v_json = {
"name":"사승원",
"age":"26",
"friend":["원승사", "승사원", {"aa":"원", "bb": "치"}]}
//자바의 Map과 유사(속성, 값)
//JSON(JavaScript Object Notation)
alert("내가 제일 좋아하는 " + v_json.friend[2].bb);
alert(v_json.name);
alert(v_json["name"]); //위와 동일
alert(v_json.age);
alert(v_json["age"]); //위와 동일

</script>
```

#### 👏 데이터타입2
```html
<!DOCTYPE html>
<meta charset="UTF-8">
<script>

var v_check = "a772"
v_check = v_check - 0 ;
alert(v_check) ; //NaN -> Not a Number : 숫자로 바뀌지 않는 문자열은 NaN이 뜸

var v_num1 = 111;
var v_num2 = 222;
alert(v_num1, v_num2) //v_num1이 내부적으로 자동으로 타입을 문자열로 바뀜
// + 는 문자열 더하기와 숫자더하기 2가지 존재, 문자열 더하기 우선
alert(v_num1/v_num2); // -,*, / 연산은 숫자형에만 존재

//질문 1 숫자형을 문자형으로 바꾸려면
var v_num3 = 333;
alert(typeof(v_num3));
v_num3 = v.num3 + ""; //숫자에 문자열(빈공백)을 더하면 문자형으로 형변환됨
alert(typeof(v_num3));
//더하기는 숫자형보다 문자형으로 우선적으로 변환

//질문 2 문자열형을 숫자로 바꾸려면
var v_str = "666";
alert(typeof(v_str));
v_str = v_str - 0; //문자열에서 - 숫자를 하면 숫자형으로 형변환됨
alert(typeof(v_str))

</script>
```

#### 👏 데이터타입3
```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>

//boolean(true/false)
//var v_bool = true;
//var v_bool = 0 //숫자는 0만 false 나머지는 모두 true
//var v_bool = ""; //문자열은 빈공백만 false 나머지는 모두 true
//var v_bool = []; // true - 빈 객체 선언
//var v_bool = {}; // true -
//모든 객체는 true;
//v_bool = null; // null = false
//v_bool = undefined; // undefined = false
if(v_bool){
alert("이 창은 뜨나요?"); //true
}else {
alert("난 엘스"); //false
}
</script>
```

#### 👏 배열
```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>

//배열 아주 중요, 자바의 Collection(List, Set, Map) - Set : 중복제거
//var v_arr = ["사승일", "사승이", "사승삼"]; //선언 : 빈배열
//alert(v_arr.length); // 배열에서 가장 중요한 속성 // 3
//alert(v_arr[2]); // 사승삼
//alert(v_arr[v_arr.length-1]); // 인덱스는 0부터 시작이라 (length -1) // 사승삼

/*
var v_arr = [] ;
v_arr[0] = "사승일";
v_arr[1] = "사승이";
v_arr[2] = "사승삼";
v_arr[3] = ["사승사", "사승오", "사승육", "사승칠"];
alert(v_arr[v_arr.length-1]) //마지막 값
*/

//위보다 더 좋은 방법 - length 속성 중요!
var v_arr = [] ;
v_arr[v_arr.length] = "사승일";
v_arr[v_arr.length] = "사승이";
v_arr[v_arr.length] = "사승삼";
v_arr[v_arr.length] = "사승사";
alert(v_arr[v_arr.length-1])


</script>
```

#### 👏 XML이란?
```xml
<?xml version="1.0" encoding="utf-8"?>

<!--
문서교환 포맷으로 나와서 내 마음대로 태그를 정할 수 있음.
당사자끼리만 룰을 알면 되니까.
설명 파일에 많이 사용됨
-->
<친구들>
<친구>
<이름>사승원</이름>
<나이>26</나이>
<별명>4win1</별명>
</친구>
<친구>
<이름>사승이</이름>
<나이>22</나이>
<별명>2win2</별명>
</친구>
</친구들>
```
## 📚 3일차
#### 👏 연산자
```html
<!DOCTYPE html>
<meta charset="UTF-8">
<script>

//연산자
//산술 연산자 : + - * / %
//조건 연산자 : &&(and), ||(or)
//AA && BB : && 연산자는 두 개 다 true여야 true라서 false인 것을 앞에 놓으면 성능 좋아짐
//AA || BB : || 연산자는 둘 중 하나만 true여도 true라서 true를 앞에 놓으면 성능 좋아짐
//증감 연산자 : ++, --, +=,-=
var i = 3 ;
var v_aa = i++; //후치연산
/*
var v_aa = i;
i = i + 1 ;
*/

i = 3;
var v_bb = ++i;
/*
i = i + 1 ;
var v_bb = i
*/

// 연산자 우선순위는 외우지 않고 ()를 활용한다

</script>

```
#### 👏 반복문1

```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>
//반복문
//for(초기치;조건;증감식) // 초기치와 증감식은 생략가능, 조건은 필수
var i = 1 ;
for(;"사승원";){ // 이렇게 사용하면 while문과 정확히 똑같음
alert("무한루프"); // 무한루핑 구현할 땐 항상 빠져나가는 조건을 설정한다.
//빠져나갈 조건
i++;
if(i>10){
alert("break가 실행됩니다.")
break;
}
}

</script>
```

#### 👏 반복문2
```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>

//일반적 사용법
//반복문은 주로 배열에서 많이 사용
//배열 반복문에서는 length 중요
//배열 반복문에서는 =(이퀄) 사용 X

// 1. for문
var v_arr = ["사승일", "사승이", "사승삼", "사승사"];
for(var i = 0 ; i < v_arr.length ; i++){
alert("안녕하세요1 " + v_arr[i] + "님");
}

// 2. while문
var i = 0;
while(i < v_arr.length){
alert("안녕하세요2 " + v_arr[i] + "님");
i++;
}

var i = 0;
while(i < v_arr.length){
if(i==2){
i++; // i++없으면 무한루핑
continue; // 아래 block 스킵, for-> 증감식, while -> 조건으로
}
alert("안녕하세요3 " + v_arr[i] + "님");
i++;
}

</script>


```

#### 👏 조건문
```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>
//조건문 -> 논리의 시작

// 1. if문
// switch 보다 if 사용 권장
// !를 자주 쓰도록 하자
if(!"사승원사승원"){ // 원래 true인걸 !를 붙여서 false로 만들면 alert 실행 안 됨
alert("옳지 않아!");
}
/*
if(조건){
}else if(조건){
}else {
}
*/
// 2. switch문
//hardware에서 사용
switch(조건) {
case "스위치스위치":
break;
default:
}

// 3. 삼항연산자 ?
// if else 문을 짧게 사용한 것
// 필수는 아니지만 적당히 잘 사용하자
var i = 3 ;
var v_arr = (i < 4)? "삼":"항";
alert(v_arr);

</script>

```


#### 👏 과제
```html
<!DOCTYPE html>
<script>
var v_aa = 33;
var v_bb = 77;
//두 변수 값 스왑

v_aa = v_aa+v_bb;
v_bb = v_aa-v_bb;
v_aa = v_aa-v_bb ;

alert("v_aa : " + v_aa + "v_bb : " + v_bb);

/*

과제 : 추가 변수(v_temp) 선언 없이 산술 연산만을 이용해 두 변수 값을 바꾸시오
var v_temp;
v_temp = v_aa;
v_aa = v_bb;
v_bb = v_temp;

*/

// for(var i = 0 ; i < v_arr.length ; i++){
// if(v_arr[i]%11 == 3){
// v_arr[i] = 77;
// }else if(v_arr[i]%11 == 7){
// v_arr[i] = 33;
// }
// }
// alert("v_aa : " + v_arr[0] + "v_bb : " + v_arr[1]);


</script>
```
## 📚 4일차

#### 함수1
```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>
//function(함수) -> 자바스크립트에서 가장 중요하다.
//함수를 사용하는 이유 -> 기본적으로 같은 코드 반복을 없애고 가독성을 높임

//함수 선언법
function f_add(p_a,p_b){ //함수 선언할 때 f_ 임의로 쓴다.
alert(p_a);
return"안녕"; // 이걸 잘 이해해야 함, 초보자들의 문제. 맨 밑줄에 생략되어 있다고 생각
}

//함수는 불러줘야 실행됨(call), 내가 호출하지 않으면 사용되지 않는다.
var v_any=f_add("사승원");
alert(v_any);

/*
### 함수(Function)선언법

선언법 1
function 함수명(매개변수1, 매개변수2....){
실행코드
return "되돌려주고싶은 값";
}

선언법 2
var 함수명 = function(매개변수1, 매개변수2....){
실행코드
return "되돌려주고싶은 값";
}
return은 함수를 종료시킨다.
return을 잘 쓰면 if/else에서 else를 없앨 수 있다.

*/

var f_add = function(p_a,p_b){
return p_a + p_b;
}
alert(f_add(3,-5)); //-2

//세 개 계산

var f_add1 = function(p_a,p_b){
return p_a + p_b;
}
alert(f_add1(f_add1(3,-5),6)); // 4

function f_check(){
alert("함수가 종료됨");
return "리턴을 만나면"; //return을 만나면 함수가 종료돼서 아래에 있는 것은 실행되지 않는다.
alert("함수가 종료됨"); //return은 함수 안에서만 사용 가능
}
f_check();//함수 콜을 해야 값이 출력됨

var v_i = 100;
function f_check1(){
if(v_i>100){
alert("최대값");
return;
}
alert("최소값");
}
f_check1(); // 함수 콜
</script>

```

#### 함수2
```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>
//함수안의 코드를보고 매개변수 타입을 짐작해야 함
//함수의 매개변수 타입으로 숫자, 문자열, 배열, JSON, 함수
//함수의 return 타입도 숫자, 문자열, 배열, JSON, 함수 뭐든 와도 됨
//함수 안에 함수가 와도 된다.
//제약사항이 거의 없다.
function f_check3(p_arr){
p_arr();
}

f_check3(f_slp);
var f_slp = function(){
alert("졸리다");
}
var f_ngm = function(){
alert ("졸립니다.");
return v_j;
}

function f_check2(p_arr){
alert("이름 : " + p_arr.name + "별명 : " + p_arr.alias);
}

var v_json = {
"name" : "사승원",
"alias" : "원승사"
}
f_check2(v_json);

// function f_check(p_arr){
// for(var i = 0 ; i < p_arr.length; i++){
// alert(i + " 번째 같은 " + p_arr[i] + "입니다");
// }
// }

// f_check(["사승1", "사승2", "사승3"]);
// f_check("문자열도 length라는 속성이 있다")

function f_check4(){
return[1,3,"사승원",{"attr":["1번","2번"]}];
}
var v_rslt = f_check4();
alert(v_rslt[3].attr[1]); // 2번을 띄우고 싶다.




</script>

```

#### 함수3
```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>
// 1
function f_check(){
return[1,3,"사승원",{"attr":["1번","2번"]}];
}
var v_rslt = f_check();
alert(v_rslt[3].attr[1]); // 2번을 띄우고 싶을 때

// 2
function f_check1(){
return{
"name":"사승원",
"alias":"4win1"
}
}
var v_rslt = f_check1();
alert(v_rslt.alias);

// 데이터 타입이 뭔지, 돌려받은 게 뭔지 확인
function f_check2(){
return function(){
alert("함수임");
}
}
var v_rslt = f_check2();
v_rslt(); // 함수 실행 '함수이름(괄호);'
</script>

```

#### 함수4
```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>

function f_cal(p_op){ //사칙연산별 초간단 함수 리턴
function f_add(p_a,p_b){
return p_a + p_b;
}

function f_sub(p_a,p_b){
return p_a - p_b;
}

function f_mul(p_a,p_b){
return p_a * p_b;
}

function f_div(p_a,p_b){
return p_a / p_b;
}

//함수 안에 함수가 와도 된다. 하지만 밖에서 직접 부를 수는 없다.
//위 함수 안에서만 사용 가능
if(p_op == "+"){
return f_add;
}

if(p_op == "-"){
return f_sub;
}

if(p_op == "*"){
return f_mul;
}

if(p_op == "/"){
return f_div;
}

}

alert(f_cal("+")(100,200)); //300
alert(f_cal("-")(100,200)); //-100
alert(f_cal("*")(100,200)); //20000
alert(f_cal("/")(100,200)); //0.5

</script>

```

#### Call By Value VS Call By Reference
```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>
//call by value, call by reference(값의 복사, 값의 참조)
//복사와 참조를 결정 짓는 건 데이터 타입
//원시타입(숫자형, 문자열형)은 복사, 객체 타입은 참조(배열, JSON) (중요)

var v_value = "난 값이야";
function f_chg(p_arg){ //복사 방식으로 동작, 원본에 손상을 못 줌
p_arg = "하하하";
alert(p_arg);
}
f_chg(v_value);
alert(v_value);

</script>

```

```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>

var v_arr = ["사승원","사승투","사승3"];
function f_chg(p_arg){ //참조방식으로 동작
p_arg[1] = "tktmddnjs";
}
f_chg(v_arr);
alert(v_arr);

</script>

```

#### 버튼
```html
<!DOCTYPE html>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>버튼</title>

<style>
/* div에 스타일 주고싶을 때 / id는 #으로 */
#id_disp{
width: 300px;
height: 300px;
border: 10px solid black;
}
</style>

</head>
<body>

<!-- 꼭 기억 : 태그사이의 값에 접근하는 속성 innerHTML -->
<div id="id_disp">
사승원 사승?
<img id="id_img" src="./img/다운로드 (1).png" width="100" height="100">
</div>

<input type="button" value="눌러주세요" onclick="f_click()">
<!-- onclick일 때 f_click이라는 함수 실행하겠다는 것-->
<script>
function f_click(){
//자바스크립트에서 id값을 이용해서 태그 객체 접근
//document는 html문서 객체를 가리킴(키워드)
var v_disp = document.getElementById("id_disp");
var v_img = document.getElementById("id_img");

//접근만 하고 나면 쉽게 다시 접근할 수 있다.
v_img.width=500;
v_img.height=500;
v_img.src = "./img/html.jpg";

console.log(v_img);
console.log(v_disp.innerHTML); //콘솔로그로 눈으로 확인 / 값 읽기

v_disp.innerHTML = v_disp.innerHTML + "<h1>버튼 누르면 원래 값에 추가</h1>"
}

</script>
</body>
</html>

```

#### 오늘의 과제
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>과제</title>
<style>
img{
border : 5px solid black;
}
</style>
</head>
<body>
<img id="img_id" src="./img/1.png" width=300 height=300> <br>
<input type= button value="다음이미지" onclick="f_next()">

<script>

var v_imgs = ["1", "2", "3", "4", "5"]
var i = 0;

function f_next(){
var v_img = document.getElementById("img_id");
i++;
if(i > v_imgs.length -1 ){ i = 0 }
v_img.src = "./img/" + v_imgs[i] + ".png";
}

//사진 순서대로 넘어가는 거

</script>

</body>
</html>
```
## 📚 5일차 
#### 👏 버튼 누르면 사진 넘기기
```html
<!DOCTYPE html>

<script>
// alert("스크립트 태그는 어디에 넣어도 상관없다.")

</script>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>과제</title>
<style>
img{
border : 5px solid black;
}
</style>

<script>
//alert("스크립트 태그는 어디에 넣어도 된다. 위에서부터 실행됨") //하지만 이렇게 쓰지는 않는다. 권장되는 위치는 바디태그 위

</script>

</head>

<body>
<script>
// alert(document.getElementById("id_img"))
// html 태그들이 다 해석되어야 접근할 수 있기 때문에 스크립트 태그를 위에 쓰면 접근하기 전이기 때문에 null이 나온다.
// 그래서 body 태그 밑에다 쓴다.
// script 태그는 몇번이 와도 상관없으나, 관례적으로 바디태그 밑에다 쓰자
</script>

<img id="img_id" src="./img/1.png" width=300 height=300> <br>
<input type= "button" value="<" onclick="f_pre()">
<input type= button value=">" onclick="f_next()">

<script> //script 태그는 일반적으로 /body태그 위에 넣음(관례)

var v_imgs = ["1", "2", "3", "4", "5"]
var v_index = 0 ;
var v_img = document.getElementById("img_id"); //함수 안에 넣지말고 밖으로 빼기
var i = 0;

function f_next(){
// var v_img = document.getElementById("img_id");
i++;
if(i > v_imgs.length -1 ){ i = 0 }
v_img.src = "./img/" + v_imgs[i] + ".png";
}

function f_pre(){
i--;
if(i < 0 ){
i = v_imgs.length -1 ;
}
v_img.src = "./img/" + v_imgs[i] + ".png";
}

//사진 순서대로 넘어가는 거

</script>
</body>
</html>

```

#### 👏 라디오
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
<style>
#id_disp{/* #으로 id 접근 */
height: 200px;
border: 3px groove;
}
</style>
</head>
<body>
<!-- radio
앞에 속성의 이름을 쓴다
name : name에 값을 주면 그룹으로 묶여 그룹 중 오직 하나만 선택이 가능
checked : 처음부터 체크되어있음(디폴트값 설정) UX(User eXprience)를 위해 필요
-->
<div id = "id_disp"></div>
남<input type="radio" name="nm_sb" value="male">
여<input type="radio" name="nm_sb" value="female">

<!-- hr : 가로줄 -->
<hr>

내국인<input type="radio" name="nm_na" value="korean">
외국인<input type="radio" name="nm_na" value="foreign"><br>
<input type="button" value="눌러보세요" onclick="f_click()">

<script>
var v_disp = document.getElementById("id_disp");
var v_sb = document.getElementsByName("nm_sb"); // 배열을 리턴해준다고 생각하면 됨
var v_na = document.getElementsByName("nm_na"); // 배열을 리턴해준다고 생각하면 됨
//console.log(v_sb[1]) //잘 모르면 찍자
var f_click = function(){
var v_msg = "당신은 ";
for(var i = 0; i < v_sb.length; i++){
//체크된 것 확인 checked된 속성이 true
if(v_sb[i].checked){
//alert("당신의 선택은 " + v_sb[i].value + " 입니다")
if(v_sb[i].value=="male"){
v_msg += " 남자입니다.";
}else{
v_msg += " 여자입니다.";
}
break; // 계속 돌기 때문에 성능에 손해 그래서 break 꼭 필요함
}
}

for(var i = 0; i < v_na.length; i++){
//체크된 것 확인 checked된 속성이 true
if(v_na[i].checked){
//alert("당신의 선택은 " + v_sb[i].value + " 입니다")
if(v_na[i].value=="kor"){
v_msg += " 내국인입니다.";
}else{
v_msg += " 외국인입니다.";
}
break; // 계속 돌기 때문에 성능에 손해 그래서 break 꼭 필요함
}

}
v_disp.innerHTML = "<h1>" + v_msg + "</h1>";
}
</script>
</body>
</html>

```

#### 👏 체크박스1
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
</head>
<body>
<!-- 체크박스는 사용자에게 여러 개 선택을 요구할 때 취미, 관심분야 등 -->
당신의 보유 스킬을 선택해주세요(다중선택가능, 3개만 선택가능) <br>
자바<input type="checkbox" name = "nm_skill" value="java">
HTML<input type="checkbox" name = "nm_skill" value="HTML">
CSS<input type="checkbox" name = "nm_skill" value="CSS">
js<input type="checkbox" name = "nm_skill" value="javascript">
SQL<input type="checkbox" name = "nm_skill" value="SQL"> <br>
<input type="button" value="체크된 값 확인" onclick="f_ckbox()">

<script>
var v_skills = document.getElementsByName("nm_skill");
//console.log(v_skills[3]); 확인
function f_ckbox(){
var v_cnt = 0 ;
var v_rslt = []; //결과를 담을 빈 배열
for(var i=0; i < v_skills.length; i++){
if(v_skills[i].checked){
v_cnt++;
// v_rslt += v_skills[i].value+ " "; // 안 좋은 소스
v_rslt[v_rslt.length] = v_skills[i].value;
//체크된 value 값만 v_rslt배열에 담아보세요
//alert("체크한 값은 " + v_skills[i].value);
}
}
//세 개 넘게 선택되면 알림
if(v_cnt > 3){
alert("4개 이상 선택했습니다.")
}
alert("당신이 체크하신 값은 " + v_rslt + " 입니다.");
}

</script>

</body>
</html>

```


#### 👏 체크박스2
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
</head>
<body>
당신의 보유 스킬을 선택해주세요(다중선택가능, 3개만 선택가능) <br>
<!-- 4개 이상 선택 시 체크박스 선택 못한다고 알려주고 선택을 자동으로 풀어주는 기능
f_ckbox(0) 을 매개변수로 function f_ckbox(p_num) p_num을 활용
-->
자바<input type="checkbox" name = "nm_skill" value="java" onclick="f_ckbox(0)">
HTML<input type="checkbox" name = "nm_skill" value="HTML" onclick="f_ckbox(1)">
CSS<input type="checkbox" name = "nm_skill" value="CSS" onclick="f_ckbox(2)">
js<input type="checkbox" name = "nm_skill" value="javascript" onclick="f_ckbox(3)">
SQL<input type="checkbox" name = "nm_skill" value="SQL" onclick="f_ckbox(4)" > <br>
<input type="button" value="체크된 값 확인" onclick="f_ckbox()">

<script>
//동작은 잘 되지만 그리 좋은 소스는 아님
var v_skills = document.getElementsByName("nm_skill");
//console.log(v_skills[3]); 확인
function f_ckbox(p_num){
var v_cnt = 0 ; //4까지 돌고 다시 0으로 초기화됨
var v_rslt = []; //결과를 담을 빈 배열
for(var i=0; i < v_skills.length; i++){
if(v_skills[i].checked){
v_cnt++;
// v_rslt += v_skills[i].value+ " "; // 안 좋은 소스
v_rslt[v_rslt.length] = v_skills[i].value;
//체크된 value 값만 v_rslt배열에 담아보세요
//alert("체크한 값은 " + v_skills[i].value);
}
}
//세 개 넘게 선택되면 알림
if(v_cnt > 3){
alert("4개 이상 선택했습니다.");
v_skills[p_num].checked = false; // 체크박스 강제 해제
}
}

</script>

</body>
</html>
 
```


#### 👏 innerHTML1
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
<style>
#id_disp{
width: 400px;
height: 400px;
border: 2px solid black;
}
</style>

</head>
<body>
<div id="id_disp"></div>
<h1 id="id_h1"></h1>
<input type="button" value="누르시오" onclick="f_wrt()">
<script>
// innerHTML 태그 중요!!
var v_disp = document.getElementById("id_disp");
var v_h1 = document.getElementById("id_h1")
function f_wrt(){
v_disp.innerHTML = v_disp.innerHTML + "<h1>안녕!</h1>";
v_h1.innerHTML = v_h1.innerHTML + "<h1>하이!</h1>";
}

</script>
</body>
</html>

```


#### 👏 innerHTML2
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
<style>
#id_disp{
width: 400px;
height: 400px;
border: 2px solid black;
}
</style>

</head>
<body>


<div id="id_disp"></div>
<!-- value에 쓰면 텍스트박스 초기값 / placeholder에 쓰면 텍스트박스에 글씨 쓰면 초기값이 자동으로 없어짐 -->
<!--
## readonly vs disabled
readonly는 value값을 서버로 보낼 수 있으나, disabled는 서버로 보낼 수 없음
물론 프로그램적으로 조작하면 보낼 수 있다.
-->
<!--
<input id = "id_txt" type="text" value="readonly로 설정하면 안 지워짐" size=10 placeholder="여기에 원하는 단을 쓰세요" readonly><br>
<input type="text" value="readonly로 설정하면 비활성됨" size=10 placeholder="여기에 원하는 단을 쓰세요" disabled><br>
-->

<input id = "id_txt" type="text" value="1" size=10 placeholder="여기에 원하는 단을 쓰세요" readonly><br>
<input type="button" value="누르시오" onclick="f_wrt()">
<script>
// innerHTML 태그 중요!!
var v_disp = document.getElementById("id_disp");
var v_txt = document.getElementById("id_txt")

// var v_num = 1; /* 1 ~ 9 */
function f_wrt(){
alert(v_txt.value); // 사용자 입력값 읽어오기
//v_txt.value = "999"; // 텍스트 박스에 값 쓰기
//id_disp에 구구단 2단 출력
var v_str = "<table border=2>"; //빈 문자열
for(var i=1; i <= 9; i++){
//tr td로 구구단을 테이블로 만들기
v_str += "<tr><td>" + v_dan + " X " + i + " = " + (v_dan* i) + "</td></tr>";
//alert(v_str); //어렵다 싶으면 눈으로 확인하자
}
v_str += "</table>";
//alert(v_str); // 항상 눈으로 확인하기
v_disp.innerHTML = v_str; //입출력 횟수가 많은 프로그램은 성능이 떨어짐!, 되도록 횟수를 줄여서
}

</script>
</body>
</html>

```


#### 👏 구구단테이블 만들기 문제
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>

<style>
#id_disp{
width: 400px;
height: 400px;
border: 2px solid black;
display: inline-block;
}
</style>

</head>
<body>
<div id="id_disp"></div>
<!-- value에 쓰면 텍스트박스 초기값 / placeholder에 쓰면 텍스트박스에 글씨 쓰면 초기값이 자동으로 없어짐 -->
<!--
## readonly vs disabled
readonly는 value값을 서버로 보낼 수 있으나, disabled는 서버로 보낼 수 없음
물론 프로그램적으로 조작하면 보낼 수 있다.
-->
<!--
<input id = "id_txt" type="text" value="readonly로 설정하면 안 지워짐" size=10 placeholder="여기에 원하는 단을 쓰세요" readonly><br>
<input type="text" value="readonly로 설정하면 비활성됨" size=10 placeholder="여기에 원하는 단을 쓰세요" disabled><br>
-->

<script>
var v_disp = document.getElementById("id_disp");
for(var i=1; i <= 9; i++){
var v_str = "<table border=2> <tr>"
for(var j = 1; j<= 9; j++){
v_str += "<td>" + i + " X " + j + " = " + (i* j) + "</td>" + "</tr>";
//alert(v_str)
}
v_str += "</table>";
v_disp.innerHTML += v_str;
}



</script>
</body>
</html>
 
```
## 📚 6일차

#### 구구단 테이블 만들기
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>

<style>
#id_disp{
width: 2000px;
height: 400px;
border: 1px solid red;
}
</style>
</head>
<body>
<div id="id_disp"></div>
<input type="button" value="누르세요" onclick="f_gugu()">

<script>
var v_disp = document.getElementById("id_disp");

function f_gugu(){
var v_tblStr = "<table border>";
for(var i=2; i<=9; i++){
v_tblStr += "<td>" + f_dan(i) + "</td>"
}
v_tblStr += "</tr></table>";
v_disp.innerHTML = v_tblStr; // 출력
}

function f_dan(p_dan){
var v_tblStr = "<table border=1>";
for(var i=1; i<=9; i++){
v_tblStr += "<tr><td>" + p_dan + " X " + i + " = " + (p_dan*i) + "</td></tr>"
}
v_tblStr += "</table>";
return v_tblStr;
}


// function f_gugu(){
// var v_tblStr = "<table border=1>";
// v_tblStr += "<tr>";

// for(var i =1; i <=9; i++){
// v_tblStr += "<tr>";
// for(var v_dan = 2; v_dan<=9; v_dan++){
// v_tblStr +="<td>" + v_dan + " X " + 1 + " = " + (v_dna*1) + "</td>";
// }
// v_tblStr += "</tr>";
// }
// v_tblStr += "</table>";
// v_disp.innerHTML = v_tblStr;
// }

</script>
</body>
</html>

```

#### 변수Scope
```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>
//자바스크립트에서 변수스코프(범위)
//전역변수, 지역변수(function 기준)
//function 안에 선언되었으면 지역변수, ()랑은 관계없음
//es5 버전 기준

var v_global = "전역변수";
function f_scope(){
var v_global = "지역변수"; // function 안에 선언된 건 function 안에서만 사용가능
}
f_scope();
alert(v_global);
</script>

```

#### SELECT
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>선택박스(콤보박스)</title>
</head>
<body>
<!-- select : 세로로 내려오는 선택창
selected : 디폴트값
<select onchange="f_chg()"> : 맨날 쓰는 거, 사용자가 선택을 변경하면 값을 바꿔라
-->

<!-- 모바일에서 select를 체크박스 대용으로 사용되고 있음
multiple : 여러 개 선택 가능하게 해줌
size : 펼쳐진 사이즈 값
-->
<select id= "id_sel" multiple size=3 onchange="f_chg()">
<option value="0">선택하세요</option>
<option value="win" selected>4win1</option>
<option value="tk">tktmddnjs</option>
<option value="sa">saseungwon</option>
<option value="ssw">사승원</option>

</select>

<script>
var v_sel = document.getElementById("id_sel")
function f_chg(){
// alert("선택하신 값은 " + v_sel.value + " 입니다.");
// 밑에 있는 쿼리를 v_sel.value 하나로 쓸 수 있다. 데스크탑에서 사용

//alert(v_sel.options[1].selected)//options는 배열이다.
//var v_opts = v_sel.options; // 줄여 쓸 수 있는 것은 오직 객체만

//multiple은 모바일에서 사용
var v_selVal = [];
for(i = 0; i< v_opts.length; i++){
if(v_opts[i].selected){
v_selVal[v_selVal.length] = v_opts[i].value;
}
}
alert("선택하신 값은 " + v_selVal + " 입니다." )
}

</script>

</body>
</html>

```

#### TEXTAREA
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
</head>
<body>
<!-- textarea : 여러 줄 입력 가능 -->
<textarea id="id_ta" cols="30" rows="10">
이건 여러 줄 입력하는 것

</textarea><br>
<input type="button" value="누르시오" onclick="f_ck()">

<script>
function f_ck(){
alert(document.getElementById("id_ta").value);

}

</script>
</body>
</html>

```

#### Math.Random
```html
<!DOCTYPE html>
<meta charset="utf-8">
<script>
//원래 지원되는 (bullt-in) Math 객체
//random
/*
for(var i = 1; i<=10; i++){
alert(Math.random()); //값 0 <= X < 1 // 0.??????????????????
}
*/

alert(Math.ceil(0.1)); // ceil : 올림 = 1
alert(Math.floor(0.9)); // floor : 내림 = 0
alert(Math.round(0.5)); // round : 반올림 = 1

//1~100사이의 랜덤한 숫자를 발생시키려면
alert(Math.ceil(Math.random()*100));
//55~100사이의 랜덤한 숫자를 발생시키려면
alert(Math.ceil(Math.random()*45)+55);

//자동 계산
function f_ran(p_start, p_end){
return Math.round(Math.random()*(p_end-p_start))+ p_start;
}
for(var i=0; i<=10; i++){
console.log(f_ran(54,111));
}
</script>

```

#### setTimeout : 비동기함수
```html
<!DOCTYPE html>
<meta charset="utf-8">
<!-- setTimeout : 비동기함수-->
<script>
//자바스크립트 대표적 비동기 함수 setTimeout

function f_ck(){
alert("안녕하세요");
}
setTimeout(f_ck,1000); /* 1000ms 뒤에 f_ck 함수를 불러오라는 의미*/
alert("setTimeout(f_ck,1000); 1000ms 뒤에 f_ck 함수를 불러오라는 의미 "); //이게 f_ck보다 먼저 뜸
</script>

```


#### 오늘의 과제(수정필요)
```html
## 수정해야됨
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>오늘의 과제</title>
</head>
<body>
<table border="1">
<tr>
<td>아이디</td>
<td><input id= "id_id" type="text" value=""></td>
</tr>

<tr>
<td>암호</td>
<td><input id= "id_pass" type="password" value=""></td>
</tr>

<tr>
<td>성별</td>
<td>
남<input type="radio" name="sb" value="m">
여<input type="radio" name="sb" value="f">
</td>
</tr>

<tr>
<td>취미</td>
<td>
자바<input type="checkbox" name="skill" value="java">
자바스크립트<input type="checkbox" name="skill" value="js">
SQL<input type="checkbox" name="skill" value="sql">
</td>
</tr>

<tr>
<td colspan="2"><textarea id="id_txt"cols=45 rows=20></textarea></td>
</tr>

<tr>
<td colspan="2"><input type="button" value="확인" onclick="f_wr()"></td>
</tr>
</table>

<script>
var v_id = document.getElementById("id_id").value ;
var v_pass = document.getElementById("id_pass").value;
var v_sb="";
for(var i = 0; i< )
= document.getElementsByName("sb").value;
var v_skills = document.getElementsByName("skill").value;
var txt = document.getElementById("id_txt").value;

function f_wr(){
document.getElementById(id_txt).value = v_id ;

}

</script>
</body>
</html>


```

#### 오늘의 과제(답)
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
</head>
<body>
<table border=1>
<tr>
<td>아이디</td>
<td><input id="id_id" type=text value=""></td>
</tr>
<tr>
<td>암호</td>
<!--password는 보안상 입력글자가 *로 보이는 text-->
<td><input id="id_pw" type=password value=""></td>
</tr>
<tr>
<td>성별</td>
<td>
남<input type=radio name="nm_sb" value="m">
여<input type=radio name="nm_sb" value="f">
</td>
</tr>
<tr>
<td>취미</td>
<td>
자바<input type=checkbox name="nm_hobby" value="java">
자바스크립트<input type=checkbox name="nm_hobby" value="js">
오라클<input type=checkbox name="nm_hobby" value="sql">
</td>
</tr>
<tr>
<td colspan=2><textarea id="id_ta" cols=45 rows=10 readonly></textarea></td>
</tr>
<tr>
<td colspan=2><input type=button value="확인" onclick="f_ok()"></td>
</tr>
</table>
<script>
var v_rsb = document.getElementsByName("nm_sb");
var v_ckhobby = document.getElementsByName("nm_hobby");
function f_ok(){
//아이디 가져오깅
var v_id = document.getElementById("id_id").value;
//암호 가져오깅
var v_pw = document.getElementById("id_pw").value;
//성별 가져오깅
var v_sb="";
for(var i=0; i < v_rsb.length; i++){
if(v_rsb[i].checked){
v_sb = v_rsb[i].value;
break;
}
}
if(v_sb=="m") v_sb="남자";
else v_sb = "여자";
//취미 가져오깅
var v_hobbis = [];
for(var i=0; i< v_ckhobby.length; i++){
if(v_ckhobby[i].checked){
v_hobbis[v_hobbis.length] = v_ckhobby[i].value;
}
}
//최종 메세지 맹글깅
// textarea에서 엔터키는 escape sequence 문자 \n
var v_finalMsg = "당신의 아이디는 " + v_id + " 이고\n\n";
v_finalMsg += "암호는 " + v_pw + " 이며\n\n";
v_finalMsg += "성별은 " + v_sb + " 이며\n\n";
v_finalMsg += "취미는 " + v_hobbis + " 이네용 맞나용?";

//최종 메세지 textarea에 출력
document.getElementById("id_ta").value=v_finalMsg;
}
</script>
</body>
</html>

```
## 📚 7일차

#### setTimeout2
```html
<!DOCTYPE html>
<meta charset="utf-8">
<!-- setTimeout : 비동기함수-->
<script>
//자바스크립트 대표적 비동기 함수 setTimeout

function f_ck(p_client){
alert(p_client + p_sec + "안녕하세요");
}
setTimeout(f_ck, 3000, "사승원", "4win1"); /* 1000ms 뒤에 f_ck 함수를 불러오라는 의미*/
alert("setTimeout(f_ck,1000); 1000ms 뒤에 f_ck 함수를 불러오라는 의미 "); //이게 f_ck보다 먼저 뜸
</script>

```


#### 재귀호출
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>재귀호출</title>
<style>
#id_disp{
height: 50px;
border : 1px solid black;
}
</style>

</head>
<body>
<div id="id_disp"></div>
<input type="button" value="누르세요" onclick="f_ck()">
<script>
//1~특정숫자까지 합을 구하는 함수
var v_disp = document.getElementById("id_disp"); // 참조방식(가능)
//var v_disp = document.getElementById("id_disp").innerHTML; // 복사방식 (불가능)

/*
function f_sum(p_num){
var v_sum = 0;
for(var i=1; i<=p_num; i++){
v_sum += i;
}
return "1부터 " + p_num + "까지 합은 " + v_sum + " 입니다";
}
*/

function f_sum(p_num){
if(p_num ==1){
return 1;
}
return p_num * f_sum(p_num-1); //자신속에서 자신을 호출(재귀호출), 무한루핑 구조라서 종료조건을 먼저 생각하고 써야됨
}
/*
f_sum(4) --> 4 + f_sum(3)
--> 3 + f_sum(2)
--> 2 + f_sum(1)
+ 1
*/
var v_i = 1;
function f_ngm(){
alert(i + "번째" + "사승원");
v_i++;
setTimeout(f_ngm, 500);
}

function f_ck(){
setTimeout(f_ngm,500); //재귀호출로 많이 사용됨
//v_disp.innerHTML = "팩토리아 5! = " + f_sum(5);
}
</script>
</body>
</html>

```


#### Position
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>

<style>
div{
width: 200px;
height: 200px;
border : 1px solid black /* 레이아웃 잡을 땐 항상 이게 있으면 도움됨 */
}
#ssw {
/* position: static; 기본값은 브라우져가 알아서 하라고 해서 밑에 값을 써도 움직이지 않음*/
/* position: relative; static으로 자리잡은 그 지점에서 설정한 값만큼 움직임*/
position: absolute;/* 브라우저 화면 왼쪽 상단 모서리 기준으로 움직임(사실 레이어가 붕 뜸) */
left: 300px;
top: 100px;
}
</style>
</head>
<body>
<div>안녕1</div>
<div id="ssw">안녕2</div>
<div>안녕3</div>
</body>
</html>

```


#### Posision2
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
<style>
div{
position: relative;
width: 150px;
height: 150px;
border: 2px solid black;
}
.ssw {
/*
부모가 relative이고 자식이 absolute일 때 자식의 좌표기준점이
부모의 왼쪽 상단 모서리로 바뀜
레이아웃 잡을 때 기본은 일단 static으로 대략 모양을 만든 다음에 relative나 absolute를 사용하는 것임
처음부터 relative나 absolute를 사용하면 뒷감당이 안됨
*/
position: absolute;
height: 30px;
border: 2px solid palevioletred;
}
.special{
top: 30px;
left: 50px;
}

</style>
</head>
<body>
<div>포지션1</div>
<!-- 태그 안에 태그를 표현할 때 바깥태그 부모(parent), 안쪽태그 자식(child)
자식의 자식 자손
-->
<div>
<div class="ssw">포지션2.1</div>
<div class="ssw special">포지션2.2</div>
<div class="ssw">포지션2.3</div>
<div class="ssw">포지션2.4</div>
</div>
<div>포지션3</div>
</body>
</html>

```


#### 벽에 튕기는 공
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
<style>
#ssw{
position: absolute; /* 움직이려면 relative나 absolute가 있어야 됨 */
width: 100px;
height: 100px;
background-color: chartreuse;
top: 150px;
left: 100px;/* inline style 값이 내부 style값보다 우선순위가 높음 */

/* 알아두면 쓸만한 css */
border-radius: 50px; /* width or height 값의 절반값을 주면 원형됨, 모서리를 둥글게 */
background-image: url("./img/공.jpeg");/*이미지 삽입*/
background-size: 120px 120px;
/* background-size: 100px 100px; */
}
.cl_bar{
position:absolute;
width:100px;
left: 600px;
height: 100vh;/* 높이 : 100퍼센트 */
background-color: crimson;
}

.cl_bar2{
position:absolute;
width:100vw;/* 넓이 : 100퍼센트 */
height: 100px;
top: 450px;
background-color: crimson;
}

</style>
</head>
<body>
<div class= "cl_bar">기둥</div>
<div class= "cl_bar2">기둥2</div>
<div id="ssw"></div>
<input type="button" value="오른쪽으로 가기" onclick="f_cont()">
<input type="button" value="그만가" onclick="f_stop()">
<script>
var v_bar = document.getElementsByClassName("cl_bar")
var v_ssw = document.getElementById("ssw");
var v_mvR = 10; /* 움직이는 폭 */
var v_mvT = 10; /* 움직이는 상하 */
var v_timer; /*지역변수를 전역변수로 만들어서 밖에서 부를 수 있게 해줌*/
//버튼 누르면 속도 빨라지는 거 안 되게 한 번만 실행할 수 있게 해주기
//직접 가는 걸 중간에 한 번 거쳐서 조건을 줘서 제어가능(proxy 패턴)
var v_run = false;
function f_cont(){
if(!v_run){
f_move();
v_run = true;

}
}

//멈추기
function f_stop(){
//clearTimeout(만든 타이머를 없애준다.) <--> setTimeout
clearTimeout(v_timer);
v_run =false;
}

//움직이기
function f_move(){
if(!v_ssw.style.left){/* 원래 빈공백인데 !로 '만약 정의되지 않았다면?'*/
v_ssw.style.left = "100px"; /* 초기값을 100px로 정의할 수 있음 단위값(px)를 꼭 줘야함*/
v_ssw.style.top = "150px";
}
//parseInt(v_ssw.style.left);
v_ssw.style.left = parseInt(v_ssw.style.left) + v_mvR + "px";
v_ssw.style.top = parseInt(v_ssw.style.top) + v_mvT + "px";

var v_left = parseInt(v_ssw.style.left);
var v_right = parseInt(v_ssw.style.left)+ 100;
var v_top = parseInt(v_ssw.style.top) ;
var v_bottom = v_top + 100;

if(v_right >= 700 || v_left <=0){// 좌우충돌
v_mvR = -v_mvR;
}

if(v_bottom >= 450 || v_top <=0){//방향 바꾸기
v_mvT = -v_mvT;
}
v_timer = setTimeout(f_move,50);//0.05초마다 버튼 누르면 자동으로 오른쪽으로 움직임
}

</script>
</body>
</html>

```


#### 오늘의 과제
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
<style>
/* *은 모든을 의미함 */
*{
margin:0;
}
#container{
margin:0 auto; /* 박스 선 수평 중앙 정렬방법 */
width: 500px;
height: 95vh;
border :1px solid black;
text-align: center; /* 박스 내부 수평 가운데 정렬 */
}
</style>
</head>
<body>
<!--
일반적으로 레이아웃 잡을 때 화면전체를 잡는 div 태그를 주고
그것의 id나 class를 container라는 이름으로 많이 줌
-->
<div id="container">
<script>
for(var i=1; i<=6; i++){
document.write("<h"+i+">난 사승원입니다!</h"+i+">");
if(i==6){
i--;
}else if(i==1){
break;
}
}
// for(var i=5; i>=1; i--){
// document.write("<h"+ i +">난 사승원입니다!</h"+ i+ ">" );
// }

// 오늘의 과제 위 for문 2개를 for 한 번만 사용해서 같은 결과가 나오도록 합니다.
// 추가적인 조건문 등의 사용은 상관없다.
</script>
</div>
</body>
</html>

```

## 📚 8일차
#### 오버플로우(overflow)
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
<style>
#id_parent{
position: relative;
left: 300px;
top: 100px;
border: 5px solid black;
width: 150px;
height: 150px;
overflow: hidden; /*overflow: hidden; 부모 영역을 벗어난 자식 감추기 */
/* overflow: scroll; 스크롤바 생김 */
/* overflow: auto; 부모 영역을 벗어나면 자동으로 스크롤바 생김*/
}
.cl_child{
display: inline-block;
width: 150px;
height: 150px;
}
#id_row1, #id_row2 {
position: absolute; /* static은 움직이지 않음 */
width: 620px;
height: 150px;
border :1px solid pink;
}
#id_row2{
left: 620px;
}

</style>
</head>
<body>
<div id="id_parent">
<div id="id_row1">
<div class="cl_child">
<img src="./img/1.png" width="150" height="150">
</div>

<div class="cl_child">
<img src="./img/2.png" width="150" height="150">
</div>

<div class="cl_child">
<img src="./img/3.png" width="150" height="150">
</div>

<div class="cl_child">
<img src="./img/4.png" width="150" height="150">
</div>
</div>

<div id="id_row2">
<div class="cl_child">
<img src="./img/5.png" width="150" height="150">
</div>

<div class="cl_child">
<img src="./img/6.png" width="150" height="150">
</div>

<div class="cl_child">
<img src="./img/7.png" width="150" height="150">
</div>

<div class="cl_child">
<img src="./img/8.png" width="150" height="150">
</div>
</div>
</div>

<input type="button" value="움직여" onclick="f_move()">
<script>
var v_row1 = document.getElementById("id_row1");
var v_row2 = document.getElementById("id_row2");
function f_move(){
if(!v_row1.style.left){//문자열 공백이 false임을 이용해서 초기화
v_row1.style.left = "0px"; //움직여야 해서 빼기
v_row2.style.left = "620px";
}
v_row1.style.left = parseInt(v_row1.style.left) - 10 + "px";
if(parseInt(v_row1.style.left)<= -620){
v_row1.style.left = "620px";
}
v_row2.style.left = parseInt(v_row2.style.left) - 10 + "px";
if(parseInt(v_row2.style.left)<= -620){
v_row2.style.left = "620px";
}
//px를 제외한 숫자를 -10 해야되니까 parseInt로 연산 후 "px" 붙여야됨
setTimeout(f_move, 10);

}


</script>
</body>
</html>

```

#### none과 visible
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
<style>
#id_disp{

/*display:block 공간도 차지하지 않고 눈에도 보이지 않음(none, block) */
/*visibility:visible; 내용이 보이진 않으나 공간은 차지(hidden, visible) */
}
</style>
</head>
<body>
<div id = "id_disp">
<h1>사승원123</h1>
</div>
<input id="id_btn" type="button" value="안 보이게" onclick="f_showhidden1()">
<script>
//Toggle은 기본이니 잘하자
var v_disp = document.getElementById("id_disp");
var v_btn = document.getElementById("id_btn")
var v_visi = true; /* 현재 보이는 상태를 true라고 지정, 초기값 */

// 이런 코드는 좋지 않음. 코드가 버튼의 value값(문자열)에 의존성을 가짐
function f_showhidden1(){
if(v_btn.value == "안 보이기"){
v_disp.style.visibility = "hidden";
v_btn.value = "보이기";
}else{
v_disp.style.visibility = "visible";
v_btn.value = "안 보이기";
}
}

function f_showhidden(){
if(v_visi){
//v_disp.style.display = "none"; // 안 보이게 style 설정
v_disp.style.visibility = "hidden";
v_btn.value = "보이기";
v_visi = false;
return; //function 종료 기능 else 필요 없어짐
}
//v_disp.style.display = "block"; // 안 보이게 style 설정
v_disp.style.visibility = "visible";
v_btn.value = "안 보이기";
v_visi = true;
}
//setTimeout(f_showhidden,500); 누르면 깜빡이는 기능

</script>
</body>
</html>

```

#### z-index
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
</head>
<style>
div{
position: absolute;
width: 150px;
height: 150px;
border:3px solid black;
}
#id_ssw1{
/*background-color:rgb(255, 0, 200);/* #ffffff */
background-color: #ff0000; /* #f00으로 써도됨. 16진수 표기법 */
z-index: 272;

}
#id_ssw2{
background-color: rgba(255,0,0,0.5) ;/* 1이면 불투명, 0이면 완전 투명, 0.5면 반투명 */
left: 75px;
top: 75px;
z-index: 337;
}
#id_ssw3{
color: royalblue;
background-color: red;
left: 100px;
top: 100px;
z-index: 1000;
}
#id_ssw4{
left: 150px;
top: 150px;
background-color: rebeccapurple;
z-index: 9999999;
}
input{
position: absolute;
top: 400px;
}
</style>
<body>
<div id="id_ssw1">사승원1</div>
<div id="id_ssw2">사승원2</div>
<div id="id_ssw3">사승원3</div>
<div id="id_ssw4">사승원4</div>
<input type="button" value="레이어 순서" onclick="f_zindex()">
<script>
var v_ssw1 = document.getElementById
function f_zindex(){
//스크립트에서 -(하이픈)은 산술연산 빼기로 인식하기 때문에
//-을 빼고 다음 글자를 대문자로 쓴다
document.getElementById("id_ssw1").style.zIndex="999999";
v_ssw1.style.zIndex

}
</script>
</body>
</html>

```

#### 오늘의 문제(수정필요)
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Document</title>
</head>
<body>
<input type="button" value="바탕화면색 랜덤하게 0.3초마다 바뀌기" onclick="f_ranColor">
<script>
var v_hexa =[];
for(var i=0; i<=9; i++){
v_hexa[hexa.length] = ""+i;
}
v_hexa[v_hexa.length] = 'a';
v_hexa[v_hexa.length] = 'b';
v_hexa[v_hexa.length] = 'c';
v_hexa[v_hexa.length] = 'd';
v_hexa[v_hexa.length] = 'e';
v_hexa[v_hexa.length] = 'f';

function f_16RanColor(){
//16진수 랜덤한 color값 리턴하도록 작성
var v_ranSu = "#";
for(var i=1; i <6;)
var v_ranSu = v_hexa[Math.floor(Math.random()*v_hexa.length)];
}
return v_ranSu;
//return "#000055";
}

function f_rgbRanColor(){
//16진수 랜덤한 color값 리턴하도록 작성
return "rgb(255,255,0)";
}

function f_ranColor(){
//body 태그는 문서에 오직 한 번만 나와야 하기 때문에 굳이 id를 주지 않아도
//아래처럼 접근할 수 있음
document.body.style.backgroundColor = f_16RanColor();
setTimeout(f_ranColor,300); //0.3초마다 재귀호출
}

</script>
</body>
</html>

```



## 📚 10일차 

#### 레이어 돌리기
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #wrapper{
            position: relative;
            top: 50px;
            margin: 0px auto; /* 수평 가운데 정렬 */
            width: 600px;
            height: 100vh;
            border: 1px solid black;
        }
        img{    /* img태그를 활용해서 모든 이미지 크기 조정 */
            width: 275px;
            height: 275px;
        }
        .cl_layer{
            position: absolute;
        }
        #id_son{
            z-index: 1000;
            /* 아이디 값으로 하는 것 말고도 여러 방법으로 특정 사진을 맨위로 올라오게 할 수 있다.  */
            /* #id_son */
            /* style="z-index: 1000;" */
            /* .class="cl_son" */
        }

    </style>
</head>
<body>
    <input type="button" value="<" onclick="f_pre()">
    <input id="id_num" type="text" size="6" value="">
    <input type="button" value=">" onclick="f_next()">
    <div id="wrapper">
        <div id="id_son" class="cl_layer" > 
            <table border="2">
                <tr>
                    <!-- 사진에 링크 : <a> 태그로 묶어주기 -->
                    <td><a href="http://naver.com"><img src="./img/son1.jpeg"></a></td>
                    <td><img src="./img/son2.jpeg"></td>
                </tr>

                <tr>
                    <td><img src="./img/son3.jpeg"></td>
                    <td><img src="./img/son4.jpeg"></td>
                </tr>

                <tr>
                    <td><img src="./img/son5.jpeg"></td>
                    <td><img src="./img/son6.jpeg"></td>
                </tr>

            </table>
        </div>

        <div class="cl_layer">
            <table border="2">
                <tr>
                    <td><img src="./img/dog1.jpeg"></td>
                    <td><img src="./img/dog2.jpeg"></td>
                </tr>

                <tr>
                    <td><img src="./img/dog3.jpeg"></td>
                    <td><img src="./img/dog4.jpeg"></td>
                </tr>

                <tr>
                    <td><img src="./img/dog5.jpeg"></td>
                    <td><img src="./img/dog6.jpeg"></td>
                </tr>

            </table>
        </div>

        <div class="cl_layer">
            <table border="2">
                <tr>
                    <td><img src="./img/river1.jpeg"></td>
                    <td><img src="./img/river2.jpeg"></td>
                </tr>

                <tr>
                    <td><img src="./img/river3.jpeg"></td>
                    <td><img src="./img/river4.jpeg"></td>
                </tr>

                <tr>
                    <td><img src="./img/river5.jpeg"></td>
                    <td><img src="./img/river6.jpeg"></td>
                </tr>

            </table>
        </div>

        <div class="cl_layer">
            <table border="2">
                <tr>
                    <td><img src="./img/pool1.jpeg"></td>
                    <td><img src="./img/pool2.jpeg"></td>
                </tr>

                <tr>
                    <td><img src="./img/pool3.jpeg"></td>
                    <td><img src="./img/pool4.jpeg"></td>
                </tr>

                <tr>
                    <td><img src="./img/pool5.jpeg"></td>
                    <td><img src="./img/pool6.jpeg"></td>
                </tr>

            </table>
        </div>

    </div>
    <script>
        var v_layers = document.getElementsByClassName("cl_layer");
        var v_num = document.getElementById("id_num");
        var v_index = 0; // 레이어 초기값,  첫 번째 레이어를 맨 위로 올려놓은 상태 
        var v_currentTop = 0; // 현재 맨위의 레이어의 index 값을 저장하는 변수 

        v_num.value = (v_index+1)+ "/" + v_layers.length; //나누기 연산이 되면 안 돼서 /를 문자열 "/"로
        
        // 레이어 수가 많으면 init 말고 v_currentTop으로 해야 효율적
        // function f_init(){
        //     for(var i=0; i < v_layers.length; i++){
        //         v_layers[i].style.zIndex = 1; //모든 레이어 zIndex값을 1로 초기화 
        //     }
        //}

        function f_next(){
            //f_init();
            v_index++;
            if(v_index > (v_layers.length -1)){
                v_index = 0;
            }
            v_num.value = (v_index+1)+ "/" + v_layers.length;
            v_layers[v_currentTop].style.zIndex = 1;
            v_layers[v_index].style.zIndex = "1000";
            v_currentTop = v_index; 
        }

        function f_pre(){
            //f_init();
            v_index--;
            if(v_index < 0){
                v_index = v_layers.length -1; //배열의 마지막 index로 
            }
            v_num.value = (v_index+1)+ "/" + v_layers.length;
            v_layers[v_currentTop].style.zIndex = 1;
            v_layers[v_index].style.zIndex = "1000";
            v_currentTop = v_index; 
        }

    </script>
</body>
</html>
```
#### 공튀기기 skew 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #ssw{
            position: absolute; /* 움직이려면 relative나 absolute가 있어야 됨 */
            width: 100px;
            height: 100px;
            background-color: chartreuse;
            top: 150px;
            left: 100px;/* inline style 값이 내부 style값보다 우선순위가 높음 */

            /* 알아두면 쓸만한 css */
            border-radius: 50px; /* width or height 값의 절반값을 주면 원형됨, 모서리를 둥글게 */
            background-image: url("./img/공.jpeg");/*이미지 삽입*/
            background-size: 120px 120px;
            /* background-size: 100px 100px; */
        }
        .cl_bar{
            position:absolute;
            width:100px;
            left: 600px;
            height: 100vh;/* 높이 : 100퍼센트 */
            background-color: crimson;
        }

        .cl_bar2{
            position:absolute;
            width:100vw;/* 넓이 : 100퍼센트 */
            height: 100px;
            top: 450px;
            background-color: crimson;
        }

    </style>
</head>
<body>
    <div class= "cl_bar">기둥</div>
    <div class= "cl_bar2">기둥2</div>
    <div id="ssw"></div>
    <input type="button" value="오른쪽으로 가기" onclick="f_cont()">
    <input type="button" value="그만가" onclick="f_stop()">
    <script>
        var v_bar = document.getElementsByClassName("cl_bar")
        var v_ssw = document.getElementById("ssw");
        var v_mvR = 10; /* 움직이는 폭 */ 
        var v_mvT = 10; /* 움직이는 상하 */
        var v_timer; /*지역변수를 전역변수로 만들어서 밖에서 부를 수 있게 해줌*/
        
        //버튼 누르면 속도 빨라지는 거 안 되게 한 번만 실행할 수 있게 해주기
        //직접 가는 걸 중간에 한 번 거쳐서 조건을 줘서 제어가능(proxy 패턴)
        var v_run = false;
        function f_cont(){
            if(!v_run){
                f_move();
                v_run = true;

            }
        }

        //멈추기 
        function f_stop(){
            //clearTimeout(만든 타이머를 없애준다.) <--> setTimeout
            clearTimeout(v_timer);
            v_run =false;
        }

        //움직이기
        function f_move(){
            if(!v_ssw.style.left){/* 원래 빈공백인데 !로 '만약 정의되지 않았다면?'*/
                v_ssw.style.left = "100px"; /* 초기값을 100px로 정의할 수 있음 단위값(px)를 꼭 줘야함*/
                v_ssw.style.top = "150px";
            }
            v_ssw.style.transform = "skewX(0deg) skewY(0deg)"
            //parseInt(v_ssw.style.left);
            v_ssw.style.left = parseInt(v_ssw.style.left) + v_mvR + "px";
            v_ssw.style.top = parseInt(v_ssw.style.top) + v_mvT + "px";

            var v_left = parseInt(v_ssw.style.left);
            var v_right = parseInt(v_ssw.style.left)+ 100;
            var v_top = parseInt(v_ssw.style.top) ;
            var v_bottom = v_top + 100; 

            if(v_right >= 700 || v_left <=0){// 좌우충돌
                v_ssw.style.transform = "skewY(45deg)"
                v_mvR = -v_mvR;
                }

            if(v_bottom >= 450 || v_top <=0){//방향 바꾸기 
                v_ssw.style.transform = "skewX(45deg)"
                v_mvT = -v_mvT;
            }
            
                v_timer = setTimeout(f_move,50);//0.05초마다 버튼 누르면 자동으로 오른쪽으로 움직임
        }
    </script>
</body>
</html>
```
#### Transform
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #id_img{
            width: 200px;
            height: 200px;
            background-image: url("./img/son1.jpeg");
            background-size: 200px 200px;
            /* border-radius: 100px; */
            /* transform: rotateX(55deg); */
            /* transform: rotate X,Y,Z(??deg) 기본값은 Z */
            transform-origin: center bottom; /* 움직임의 기준점 : transform-origin: 돌리고싶은 기준에 따라 right bottom top 등..*/
            /* transform:translateX(200px)translateY(200px); 사진 위치 설정*/
            transform: skewX(45deg); /*X축 기준으로 45도 비틀기*/
            border: 10px solid black;
            
        }

    </style>
</head>
<body>
    <div id="id_img"></div>
    <input type="button" value="누르세요" onclick="f_rot()">
    <script>
        var v_gak = 0;  //초기 각도 값 10
        var v_gakInc = 10; // 증가값 10
        var v_img = document.getElementById("id_img");

        function f_rot(){
            v_gak = (v_gak + v_gakInc) % 360; // 360이 넘어가는 값  
            v_img.style.transform= "rotate(" + v_gak + "deg)";
            setTimeout(f_rot,200);
        }
    </script>
</body>
</html>
```
#### 문자열 
```html
<!DOCTYPE html>
    <meta charset="UTF-8">
<script>
    /*
    자바 스크립트에서는 문자열 변수에 .을 찍어서 속성이나 메소드를 사용하는 순간 
    원시타입 문자열이 문자열 객체로 자동 변환됨 
    */
    var v_str = " Hello String";
    // alert(v_str.length); 
    // alert(v_str.charAt(1));
    // alert(v_str[11]); 
    // v_str[2] = 'K';  //원시 타입 데이터는 일부분을 가져올 수 있는데 일부분만 수정할 수는 없음 
    // alert(v_str);
    
    v_str.indexOf("ing"); //v_str안에 ing 문자열이 있는지 찾아라 
    alert(v_str.indexOf("ing"));
    //alert(v_str.indexOf("egg"));
    //-1은 true라는 것 잊지 말기 


    v_str.replace("Hello", "Hi^-^"); //replace는 원본을 바꾸지 않는다. 
    alert("원본 " + v_str); //Hello String

    v_str = v_str.replace("Hello", "Hi^-^"); //원래 문자열을 새로운 문자열에 넣어서 바꿔야됨 
    alert("바뀐 문자열 " + v_str); //원본 Hi^-^ String

    var v_arr = v_str.split("ll"); //return 값이 배열 
    for(var i=0; i < v_arr.length; i++){
        alert(v_arr[i]); 
        //He
        //o String
    }

    //substr : 부분추출 
    alert(v_str.substr(1,3)); // 부분추출(ell)

    //trim : 공백제거 
    alert("체크" + v_str + "체크") // 공백 확인(체크 Hello String체크)
    alert("체크" + v_str.trim() + "체크") // 공백 확인(체크Hello String체크)


</script>
```
#### 오늘의 문제 
```html
<!DOCTYPE html>
    <meta charset="UTF-8">
    <script>
    // 문제 : 모든 악마가 천사로 바뀌게 해보세요
    var v_str2 = "박태환 악마 박대환 악마 박태환 앙마 악마 악마";

        for(;v_str2.indexOf("악마") != -1;){
            v_str2 = v_str2.replace("악마", "천사")
        }
        alert(v_str2);
    /*
    v_str2 = v_str2.replace("악마", "천사");
    v_str2.indexOf("악마")
    alert(v_str2.indexOf("악마"))   //11

    v_str2 = v_str2.replace("악마", "천사");
    v_str2.indexOf("악마")
    alert(v_str2.indexOf("악마"))   //21

    v_str2 = v_str2.replace("악마", "천사");
    v_str2.indexOf("악마")
    alert(v_str2.indexOf("악마"))   //24

    v_str2 = v_str2.replace("악마", "천사");
    v_str2.indexOf("악마")
    alert(v_str2.indexOf("악마"))   //-1
    //-1은 true라는 것 잊지 말기 
    */

        // 이렇게 함수로 만들어 놓으면 편함 
        function replaceAll(p_str,p_won, p_rep){
        for(;p_str.indexOf("악마") != -1;){
            p_str = p_str.replace(p_won, p_rep);
        }
        return p_str;    
    }
    alert(replaceAll("안농 안넝 안농 안넝 히히히", "넝", "농"));
</script>
```

#### 오늘의 문제2(수정 필요)
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #id_curtain{
            width: 300px;
            border: 20px groove gold;
        }
    </style>
</head>
<body>
    <div id="id_curtain"></div>
    <script>
        var v_curtain = document.getElementById("id_curtain");
        function f_large(){
            if(!v_curtain.style.height){
                v_curtain.style.height = "0px";
            }
            v_curtain.style.height = parseInt(v_curtain.style.height) + 10 + "px";
            setTimeout(f_large,100);
        }
        f_large(); //함수 실행 
    </script>
</body>
</html>
```

## 📚 11일차 

#### 어제의 문제 정답 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #id_curtain{
            width: 300px;
            border: 20px groove gold;
        }
        #id_ssw{
            display: none;
            height: 400px;
        }
    </style>
</head>
<body>
    <div id="id_curtain">
        <div id="id_ssw">
            <h1>오늘의 문제</h1>
        </div>
    </div>
    <script>
        var v_curtain = document.getElementById("id_curtain");
        var v_heighLimit = 400;
        function f_large(){
            if(!v_curtain.style.height){
                v_curtain.style.height = "0px";
            }
            v_curtain.style.height = parseInt(v_curtain.style.height) + 10 + "px";
            if(parseInt(v_curtain.style.height) >= v_heighLimit) {
                document.getElementById("id_ssw").style.display ="block";
                return; // 함수 종료(리턴 잘쓰자)
            }
            setTimeout(f_large,100);
        }
        f_large(); //함수 실행 
    </script>
</body>
</html>
```
#### 시험 문제 내기
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .cl_dap{
            display: none;
        }
    </style>
</head>
<body>
    <h1>시험</h1>
    <input type="hidden" id="id_randap" value="">
<script>
    var v_munjesu = 5; // 전체 문제수 
    var v_cnt=4; //몇지선다형인지 쉽게 바꿀 수 있다.
    var v_jungdap = []; // 정답 배열 


    //화면 모양 만들기 
    for(var i=0; i< v_munjesu; i++){
        v_jungdap[v_jungdap.length] = Math.ceil(Math.random()*4);
    }
    document.getElementById("id_randap").value = v_jungdap; // 잠시 세이브 

    for(var j=1; j <= v_munjesu; j++){
        document.write("문제"+ j +"<hr>");
        for(var i=1; i<=v_cnt; i++){
            document.write(i+"<input type=radio name=munje"+j+ " value="+ i + ">");
        }
        document.write("<input type=text class=cl_dap name=nm_dap value='정답: ' size=5>")
        document.write("<br><br>");
    }


    //텍스트 박스에 정답 담아두기 
    var v_txtDaps =document.getElementsByName("nm_dap");
    for(var i=0; i< v_txtDaps.length; i++){
        v_txtDaps[i].value = v_txtDaps[i].value + v_jungdap[i];
        
    }
</script>
점수<input type="text" id="id_disp" value="" size="5">
<input type="button" value="채점" onclick="f_test()">
<script>
    var v_disp = document.getElementById("id_disp");
    function f_test(){
        var v_userDap= []; // 사용자 답을 담을 빈 배열 
        var v_mun1 = document.getElementsByName("munje1"); //라디오버튼 4개
        for(var i=0; i<v_munjesu; i++){
            var v_rdoGrp = document.getElementsByName("munje"+(i+1));
            for(var j=0; j<v_rdoGrp.length; j++){
                if (v_rdoGrp[j].checked){
                    v_userDap[v_userDap.length] = v_rdoGrp[j].value;
                    break;
                }
            }
        }
        if(v_userDap.length != v_munjesu){
            alert("모든 문제를 풀어주세요");
            return; // 강제 종료
        }

        //사용자 답이 정답인지 체크해서, 정답이면 카운트 
        var v_jungCnt = 0; 
        for(var i=0; i< v_munjesu; i++){
            v_txtDaps[i].style.display = "inline-block"; 
            if(v_userDap[i] == v_jungdap[i]){
                v_txtDaps[i].style.backgroundColor = "rgb(95, 173, 121)";
                v_txtDaps[i].style.color = "white";
                v_jungCnt++; // 맞혔으면 카운트 증가 
            }else{
                v_txtDaps[i].style.backgroundColor = "red";
                v_txtDaps[i].style.color = "white";
            }
        }
        //점수 출력
        v_disp.value = (v_jungCnt / v_munjesu) * 100;

        //텍스트박스에 점수가 나오도록 하기
    }
</script>
    <!-- <hr>
    1<input type="radio" name="exam1" value="1">
    2<input type="radio" name="exam1" value="1">
    3<input type="radio" name="exam1" value="1">
    4<input type="radio" name="exam1" value="1"> -->
</body>
</html>
```

#### document.write
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>난 최고의 프로그래머</h1>
    <input type="button" value="누르세요" onclick="f_check()">
    <script>
        document.write("<h2>이건 잘 나와</h2>")
    </script>
    <script>
        function f_check(){
            document.write("무슨 일이 일어날까요?");// 문서를 새로 씀 -> 원래 있던 거 없어짐
            // document.write 사용에 주의, 문서가 닫히고 나서, 문서를 쓰면 새로 써짐 
            // 그래서 잘 쓰는 사람 아니면 권장하지 않음
        }

    </script>
</body>
</html>
```

#### window
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        //자주 쓰는 onload, onsize 기억 
        //브라우저가 밑에 까지 해석이 끝나면 onload가 뜬다. 
        window.onload = function(){
            alert(document.getElementById("id_btn"));
        }
        //윈도우 사이즈가 변경되었을 때 발생하는 이벤트 
        window.onresize = function(){
            console.log("window넓이 : " + window.innerWidth);
            console.log("window높이 : " + window.innerHeight);
        }
    </script>
</head>
<body>

    <input id="id_btn" type="button" value="윈도우 사이즈 확인" onclick="f_check()">

    <script>
        var v_btn = document.getElementById("id_btn");
        v_btn.onclick = function(){
            alert("window.onload를 보니 영감이 떠올랐다.")
        }

        v_btn.onclick = f_check; 

        alert("보이는 화면 넓이 " + window.innerWidth);
        v_btn.onclick = f_check; // ()를 붙이면 함수가 그냥 실행되어 버려서 주의 
        alert("보이는 화면 넓이 " + window.innerHeight);
        return;


        function f_check(){
        //window에서 자주 쓰는 속성
        alert("보이는 화면 넓이" + window.innerWidth);
        alert("보이는 화면 높이" + window.innerHeight); 
        }

        // 엄청 많이 쓰는 이벤트
            //브라우저가 밑에 까지 해석이 끝나면 onload가 뜬다. 
            //위에서 정의한 onload가 밑에서 다시 정의되면 덮어써진다.
        window.onload = function(){
            alert("문서 로딩이 끝났습니다. 더 할 게 있으신가요?");
        }
    </script>
    
</body>
</html>
```

#### 세 가지 창
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        //document --> html문서 객체 
        //window 키워드 --> 브라우저 객체를 가리킴 
        window.alert("원래는 window. 하고 써야되는데 생략한 것")
        window.document.window("<h1>document의 부모는 window다</h1>")

        //자바스크립트는 세 가지 창을 지원한다. 
        //안 예뻐서 잘 쓰진 않지만 회사 프로그램에서는 자주 씀 

        //1.
        alert("메세지 창 : 안 예뻐서 디버깅에만 많이 사용함")

        //2.
        var v_userInput = prompt("사용자 입력창", "초기값");
        //확인 아니고 취소 버튼 누르면 null값이 들어오는 것에 주의
        alert("입력한 값은 " + v_userInput + " 입니다");

        //3. 
        var v_userCheck = confirm("말 그대로 yes or no"); 
        alert(v_userCheck); //확인 누르면 true, 취소 누르면 false
        
        

    </script>
    
</body>
</html>
```

#### 오늘의 과제
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>

    <style>
        #id_ssw{
            position: relative; /* position의 디폴트는 static이라서 안 움직임*/
            width: 200px;
            height: 200px;
            background-image: url(./img/son3.jpeg);
            background-size: 200px 200px;
            
        }
    </style>
</head>
<body>
    <div id="id_ssw" ></div>
    <script>
        //onload, onresize, innerWidth, innerHeight를 이용해서 이미지가 항상 가운데에 있도록 해보기
        //브라우져 사이즈를 변경해도 가운데 있게 하기 

        var v_imgW = 200; //이미지 넓이 설정한 값
        var v_imgH = 200; //이미지 높이 설정한 값
        
        var v_wdt = window.innerWidth
        var v_hgt = window.innerHeight

        var v_img = document.getElementById("id_ssw");
        window.onload = function(){
            v_img.style.top = (v_wdt + v_imgW)/2
            v_img.style.left = (v_hgt + v_imgH)/2
        }
        window.onresize = function(){
            console.log("window넓이 : " + window.innerWidth);
            console.log("window높이 : " + window.innerHeight);
        }
        
    
    </script>
</body>
</html>
```

## 📚 12일차 

#### frameset1
```html
<meta charset="UTF-8">
<!-- 엄청 악용되어서 범용사이트에는 거의 사용되지 않는 태그 -->
<frameset rows="50%,*">
    <frame src="./newWin1.html">
    <frameset cols="33%,33%,*">
        <frame src="./newWin.html">
        <frame src="./newWin.html">
        <frame src="./newWin.html">
    </frameset>
</frameset>
```

#### newWin
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    #id_disp {
        border:1px solid gold;
    }
</style>
</head>
<body>
    <div id="id_disp"></div>
    메세징 <input id="id_txt1" type=text value=""><br>
    <input id="id_btn" type=button value="전달">
    <input type="button" value="창 닫기" onclick="f_wClose()">
<script>

    function f_wClose(){
        //opener.v_newWin = null;
        //window.close();
        opener.f_wClose();
    }

    var v_btn = document.getElementById("id_btn");
    var v_txt1 = document.getElementById("id_txt1");
    function f_clk(){
        // 열린 윈도우는 넘겨받은 값이 없어서 누가 열어주었는지 개발자는 알수 없어용
        // 그래서 준비된 키워드 ? opener
        opener.document.getElementById("id_txt2").value = v_txt1.value;
        opener.document.getElementById("id_disp").innerHTML +=
                              v_txt1.value + "<br>";
    }
    v_btn.onclick = f_clk;
</script>    
</body>
</html>
```

#### newWin1
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    #id_disp {
        border:1px solid gold;
    }
</style>
</head>
<body>
    메세징 <input id="id_txt1" type=text value=""><br>
    <input id="id_btn" type=button value="전달">
    <input type="button" value="새창" onclick="f_new()">
<script>
    function f_new(){
        window.open("newWin2.html","aaa","width=200, height=200,left=100"); 
    }

    var v_btn = document.getElementById("id_btn");
    var v_txt1 = document.getElementById("id_txt1");
    function f_clk(){
        //부모 키워드 
        parent.frames[2].document.getElementById("id_txt1").value = 
         v_txt1.value; 
    }
    v_btn.onclick = f_clk;
</script>    
</body>
</html>
```
#### newWin2
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    #id_disp {
        border:1px solid gold;
    }
</style>
</head>
<body>
    메세징 <input id="id_txt1" type=text value=""><br>
    <input id="id_btn" type=button value="전달">
<script>
    var v_btn = document.getElementById("id_btn");
    var v_txt1 = document.getElementById("id_txt1");
    function f_clk(){
        opener.parent.frames[3].document.getElementById("id_txt1").value = v_txt1.value;
    }
    v_btn.onclick = f_clk;
</script>    
</body>
</html>
```

#### WindowOpen
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #id_disp {
            border:1px solid gold;
        }
    </style>
</head>
<body>
    <div id="id_disp"></div>
    <input id="id_btn" type=button value="새 창 열기"><br>
    메세지<input id="id_txt2" type=text value=""><br>
    <input id="id_btn1" type=button value="전달">
    <input type="button" value="창 닫기" onclick="f_wClose()">
<script>
    function f_wClose(){
        v_newWin.close();//안 닫힌다. 스크립트로 연 창만 기본적으로 닫힌다.
    }

    var v_btn1 = document.getElementById("id_btn1");
    var v_txt2 = document.getElementById("id_txt2");

    v_btn1.onclick= function(){
        if(!v_newWin){ //null이면?
            alert("새 창을 열고 전달해주세요!");
            return;
        }
        v_newWin.document.getElementById("id_txt1").value = v_txt2.value;
        v_newWin.document.getElementById("id_disp").innerHTML +=
                              v_txt2.value + "<br>";
    }

    var v_btn = document.getElementById("id_btn");
    var v_newWin =null;
    v_btn.onclick = function(){
            //window.open은 세 가지의 매개변수를 가진다

            //두 번째 자리에 있는 매개변수는 window의 name 파라미터로 지정해주면 
            //이미 그 이름으로 열린 윈도우가 있으면 그 윈도우로 감(더 이상 새로운 창이 열리지 않는다는 뜻)

            //세 번째 자리에 있는 매개변수는 위치, 크기를 설정할 수 있다. 
            //많이 악용되었던 메소드로, 점점 제약사항이 많아지고 있다. 
        v_newWin=window.open("newWin.html","ngm","width=200,height=200,left=100,top=100");
    }
</script>    
</body>
</html>
```

#### 디자이너 관점에서 본 Class
- emmet 축약기법
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .fgYellow{
            color: yellow;
        }
        .fgBlue{
            color: blue;
        }
        .bgRed{
            background-color: red;
        }
        .bgGold{
            background-color: gold;
        }
        .bgMagenta{
            background-color: magenta;
        }
    </style>
</head>
<body>
    <!-- table>tr*8>td*4 emmet 축약기법-->
    <table>
        <tr>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
    </table>

    <div class="fgBlue bgMagenta">사승원1</div>
    <div class="fgGreen bgRed">사승원2</div>
    <div class="bgMagenta">사승원3</div>
    <div class="fgYellow">사승원4</div>
</body>
</html>
```

#### overflow : hidden을 이용해 도형 자르기

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #id_what{
            overflow: hidden;/* 부모 벗어난 자식 잘라내버리기 */
            position: relative;
            left: 100px;
            top : 100px;
            width: 200px;
            height: 200px;
            /* border:1px solid black; */
            transform: rotate(45deg);
        }
        .cl_common{
            position: absolute;
            width: 200px;
            height: 200px;
            border-radius: 100px;
            background-color: red;
        }
        .cl_one{
            left: 100px;
        }
        .cl_two{
            top: 100px;
        }
    </style>
</head>
<body>
    <div id="id_what">
        <div class="cl_one cl_common"></div>
        <div class="cl_two cl_common"></div>

    </div>
</body>
</html>
```

#### 오늘의 과제(수정필요)
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>

    <style>
        #id_ssw{
            position: relative; /* position의 디폴트는 static이라서 안 움직임*/
            width: 200px;
            height: 200px;
            background-image: url(./img/son3.jpeg);
            background-size: 200px 200px;
            
        }
    </style>
</head>
<body>
    <div id="id_ssw" ></div>
    <script>
        //onload, onresize, innerWidth, innerHeight를 이용해서 이미지가 항상 가운데에 있도록 해보기
        //브라우져 사이즈를 변경해도 가운데 있게 하기 

        var v_imgW = 200; //이미지 넓이 설정한 값
        var v_imgH = 200; //이미지 높이 설정한 값
        
        var v_wdt = window.innerWidth
        var v_hgt = window.innerHeight

        var v_img = document.getElementById("id_ssw");
        window.onload = function(){
            v_img.style.top = (v_wdt + v_imgW)/2
            v_img.style.left = (v_hgt + v_imgH)/2
        }
        window.onresize = function(){
            console.log("window넓이 : " + window.innerWidth);
            console.log("window높이 : " + window.innerHeight);
        }
        
    
    </script>
</body>
</html>
```

## 📚 13일차
#### 지도 넣기
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

	<!-- 구글지도 -->
	<iframe 
	src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3214.441871184756!2d127.
	40566361568301!3d36.325839280049074!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3
	!1m2!1s0x356549345c9bfbff%3A0xad60c4c84fd8e918!2z7KSR64-E7J2867O0!5e0!3m2!1sko!2
	skr!4v1615162655723!5m2!1sko!2skr" 
	width="600" height="450" style="border:0;" allowfullscreen="" loading="lazy">
	</iframe>


    <!-- * 카카오맵 - 지도퍼가기 -->
<!-- 1. 지도 노드 -->
<div id="daumRoughmapContainer1615162219999" class="root_daum_roughmap root_daum_roughmap_landing"></div>

<!--
	2. 설치 스크립트
	* 지도 퍼가기 서비스를 2개 이상 넣을 경우, 설치 스크립트는 하나만 삽입합니다.
-->
<script charset="UTF-8" class="daum_roughmap_loader_script" src="https://ssl.daumcdn.net/dmaps/map_js_init/roughmapLoader.js"></script>

<!-- 3. 실행 스크립트 -->
<script charset="UTF-8">
	new daum.roughmap.Lander({
		"timestamp" : "1615162219999",
		"key" : "24q3v",
		"mapWidth" : "640",
		"mapHeight" : "360"
	}).render();
</script>
</body>
</html>
```

#### 유튜브 영상 넣기
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    	<!-- 유튜브 영상 넣기  -->
		<!-- 
			구글 정책으로 인해 동영상은 음소거 모드일 때만 자동실행이 가능
			무분별한 광고영상으로 사용자가 시끄러움에 지칠 수 있고
			원치 않는 상황에 빠질 수 있음에 그렇게 했다고 주장 
		 -->
	<iframe id="id_hms" width="1280" height="720" 
    src="https://www.youtube.com/embed/h5be6g38nfg?autoplay=1" 
	frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media;
	 gyroscope; picture-in-picture" allowfullscreen>
	</iframe>
	<input type="button" value="누르세요" onclick="f_next()">
	<script>
		//중복되는 값을 변수로 지정
		var v_utube = document.getElementById("id_hms"); 
		var v_urlS = "https://www.youtube.com/embed/";
		var v_urlE = "?autoplay=1"; 
		var v_list = ["h5be6g38nfg", "SJJDSUNVIS4", "n7e_Ek2g7FM"];
		var v_index = 0; 

		function f_next(){
			v_index++;
			if(v_index > (v_list.length -1)){ // 마지막 영상에서 다음 누르면 첫 영상으로 가게 
				v_index = 0; 
			}
			v_utube.src = v_urlS + v_list[v_index] + v_urlE; 
		}
	</script>

</body>
</html>
```

#### iframe 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    텍스트상자<input id="id_txt" type="text" value="난 iframe에 있어요"><br>
             <input type="button" value="버튼" onclick="f_check()">
    <script>
        var v_txt = document.getElementById("id_txt");
        function f_check(){
            //console.log(window.parent.document);
            window.parent.document.getElementById("id_txt").value = v_txt.value; 
        }
    </script>
</body>
</html>
```

#### 배열 정리 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>//indexof, push, splice 꼭 기억
    
        //매개변수가 1개 밖에 오지 않고 그것이 숫자일 때만 주의 
        //var v_arr = new Array(3,7,9,10); //[3,7,9,10] - 권장되지 않는 선언법 
        var v_arr = [3,7,9,10];  // 이 표기법이 권장됨 
        var v_arr = []; 
        v_arr[v_arr.length] = 3;
        v_arr[v_arr.length] = 7;
        v_arr[v_arr.length] = 9;
        v_arr[v_arr.length] = 10;
        //v_arr[v_arr.length] = 337;
        v.arr.push(337); // 위 주석라인과 정확히 같은 기능함 

        //꼭 기억해야 할 메소드 splice, 중간 배열요소 없애기 
        v_arr.splice(2,1); // index 2번부터 1개를 지워라 
        
        alert(v_arr.pop());// pop은 마지막 index값을 되돌려주고, 없애버림 
        alert("갯수 : " + v_arr.length + " 값들 " + v_arr);

        // 자주 쓰는 메서드 
        alert(v_arr.indexOf(10)); // 찾으면 해당 값의 index, 못 찾으면 -1  

        // alert(v_arr.length);
        // alert(v_arr); 
    </script>    
</body>
</html>
```


#### 배열 1
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="id_disp"></div>
    <input type="button" value="체크" onclick="f_check()">
    <script>
        var v_arr = [10,33,22,11,66,99,27];
        var v_mxnum = v_arr[0]; // 배열의 첫 번째 값이 최대값이라고 가정  
        function f_check(){
            for(var i = 1; i <v_arr.length; i++){
                if(v_arr[i] > v_mxnum){
                    v_mxnum = v_arr[i];
                }
            }
            document.getElementById("id_disp").innerHTML = "최대값은 " + v_mxnum; 
            //위 배열에서 최대값을 찾아서 id_disp에 출력되도록 해보세요 
            //힌트 swap(바꾸기)를 사용 
        }
    </script>
</body>
</html>
```


#### 배열 2
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="id_disp"></div>
    <input type="button" value="정렬" onclick="f_repeatRemove()">
    <script>
            var v_arr = [22,33,22,11,66,99,27,22,77,22,33,98,76];
        function f_repeatRemove(){
            //v_arr 에서 반복되는 값을 제거해서 id_disp에 출력해보세요 
            //중복제거 로직은 아주 중요, 아주 흔하게 접하게 됨 
            var v_rslt = []; //중복되지 않은 값만을 담을 배열 
            for(var i=0; i< v_arr.length; i++){ //같은 게 없다고 가정 
                var v_isRepeat = false; 
                for(var j=0; j<v_rslt.length; j++){ // 각각의 중복여부 체크를 위한 
                    if(v_rslt[j] == v_arr[i]){
                        v_isRepeat = true;
                        break; //찾았으면 검색할 필요 없음 
                    }
                }
                //없다는 가정이 맞을 때만 v_rslt에 해당 값을 넣음 
                if(!v_isRepeat){
                    v_rslt.push(v_arr[i]); 
                }
            }
            document.getElementById("id_disp").innerHTML = v_rslt;
            /* 내 오답 
            for(var i = 1; i <v_arr.length; i++){
                if(v_arr.indexOf(i) != -1){
                    v_arr.splice(2,1);
                    var count = (temp.match(v_arr[i])).length;
                    alert(count);
                    
                }
            }
            */
        }
    </script>
</body>
</html>
```


#### 배열 3 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="id_disp"></div>
    <input type="button" value="정렬" onclick="f_repeatRemove()">
    <script>
        //이중 for문식으로 복잡해 보이면, 쪼개서 함수를 만들어본다. 
        //재사용성도 높아지고, 가독성도 높아진다.항상 간단한 방법에 대해 생각 
            var v_arr = [22,33,22,11,66,99,27,22,77,22,33,98,76];
        function f_isRepeat(p_arr, p_val){
            for(var i=0; i<p_arr.length; i++){
                if(p_arr[i] == p_val){
                    return true;    //같은 게 있다면 true 리턴 
                }
            }
            return false;           //같은 것을 못 찾았다면 false; 
        }

        function f_repeatRemove(){
            var v_rslt = []; //중복되지 않은 값만을 담을 배열 
            for(var i=0; i< v_arr.length; i++){ //같은 게 없다고 가정 
                    if(!f_isRepeat(v_rslt, v_arr[i])){
                        v_rslt.push(v_arr[i]);
                    }
                }
                document.getElementById("id_disp").innerHTML = v_rslt;
        }
    </script>
</body>
</html>
```

#### 오늘의 과제
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <input id="id_txt" type="text" value="숫자를 입력하세요">
    <script>
        // 시간 : 1 2 3 4 5 6 7 8 9 10 11
        // 거리 : 3 1 4 2 5 3 6 4 7 5 8
    function f_distance(p_sec){
        var v_dist = 0 ;
        for(var i = 1; i <= p_sec; i++){
            if(i%2 ==0){
                v_dist = v_dist -2;
            }else{
                v_dist = v_dist +3; 
            }
        }
        return v_dist;
    }
    //f_distance();

    function f_sec(p_dist){
        
    }
    </script>
</body>
</html>
```

## 📚 14일차
#### CSS
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!--
        외부 사이트 css 파일 가져다 쓸 때 주의점
        https로 가져온건 스크립트로 읽을 수 있지만, http로 가져온건 못 읽음
        보안 사건이 있었음.
    
    <link rel="stylesheet" href="https://pm.pstatic.net/dist/css/nmain.20210224.css">
    -->
    <script src="./js/myfirst.js"></script>
    <link rel="stylesheet" href="./css/main.css">
    <title>Document</title>
<style>
/*내부 스타일 */
.cl_ksm {
    color:olive;
}
.cl_sya {
    color:skyblue;
}
</style>
<style>
    /*내부 스타일 */
    .cl_yhj {
        color:olive;
    }
    .cl_yuh {
        color:skyblue;
    }
</style>    
</head>
<body>
    <!-- 태그에 직접 정의한 스타일을 inline 스타일이라고 부름
        기본 우선순위 inline > 내부 > 외부
    -->
    <div class="cl_sya">오성현</div>
    <div class="cl_ygy">박태환</div>
    <input type=button value="바꾸깅" onclick="f_chg()">
<script>
    /* 일반적으로 웹 컴포넌트를 만드는 전문회사가 아니면 
       내/외부 스타일 접근법을 잘 사용하지 않음 
    */
   //일반적인 사용법 
   
   // alert(document.styleSheets[1].cssRules[1].style.color);

    //내부/외부 스타일시트 접근법
    /*
    alert(document.styleSheets[0].cssRules[0].selectorText);
    alert(document.styleSheets[0].cssRules[0].cssText);
    alert(document.styleSheets[0].cssRules[0].style.color);
    alert(document.styleSheets[0].cssRules[0].style.backgroundColor);
    */
</script>
</body>
</html>
```

#### 마우스 이벤트 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #wrapper{
            width: 95vw;
            height: 95vh;
            border: 1px solid black; 
        }
        #id_small{
            width: 200px;
            height: 200px;
            background-color: chartreuse;
        }
    </style>
</head>
<body>
    <!-- 
        body 태그에는 이벤트를 거의 걸지 않음
     -->
     <div id="wrapper" onmousedown="f_msdown()">
        <div id="id_small" onmouseover="f_msover()" onmouseout="f_msout()"></div>
    </div>
    <script>
        //마우스 버튼이 벗어날 때 
        function f_msout(){
            //alert("마우스가 벗어났습니다.")
            document.getElementById("id_small").style.backgroundImage = 
            "url(./img/son2.jpeg)";
            document.getElementById("id_small").style.backgroundSize = 
            "200px 200px";

        }
        //마우스 버튼이 올라왔을 때 
        function f_msover(){
            document.getElementById("id_small").style.backgroundImage = 
            "url(./img/son1.jpeg)";
            document.getElementById("id_small").style.backgroundSize = 
            "200px 200px";

            //alert("마우스를 올리면 알림")
        }
        function f_msdown(){
            //alert(event.button); // which 보단 직관적인 button을 더 많이 씀 
            //alert(event.which); 
        }
    </script>
</body>
</html>
```

#### 정렬 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var v_arr = [5,3,4,6,9,7,4,1,2]; 

        alert(v_arr.sort()); // 기본 오름차순으로 리턴

        alert(v_arr.sort(function(a,b){
            return a - b ;// 오른차순 
            return b - a ;// 내림차순 
        }));


    </script>
    
</body>
</html>
```

#### 버블정렬
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        //버블정렬
        var v_arr = [5,3,4,6,9,7,4,1,2]; 
        for(var j = 0; j < v_arr.length; j++){
            for(var i = j+1; i< v_arr.length; i++){
                if(v_arr[j] < v_arr[i]){
                    var v_temp = v_arr[j];
                    v_arr[j] = v_arr[i];
                    v_arr[i] = v_temp;
                }
        }
        alert((j+1) + " 번째 " + v_arr); 
        }
        alert("최종결과 : " + v_arr); 
 
    </script>
    
</body>
</html>
```

#### 콜백함수 
```html
<!DOCTYPE html>
<meta charset="UTF-8">
<script>
    //callback function
    function f_pth(){
        alert("콜백함수");
    }

    function f_check(p_func){
        p_func
    }

    f_check(f_pth); 
    // f_check를 불렀는데 f_check가 p_func을 불렀다.
    // p_func가 실행됨

    
    //익명함수.. 하나만 쓸 때는 이렇게도 쓴다. 
    f_check(function(){
        alert("콜백함수");
    }); 

    
</script>
```

#### 콜백함수로 정렬
```html
<!DOCTYPE html>
<meta charset="UTF-8">
<script>
        var v_arr = [5,3,4,6,9,7,4,1,2]; 
        v_arr.mySort = function(p_func){  // 이해를 위해서 기존 배열에 메소드 추가 
            for(var j = 0; j < this.length; j++){
                for(var i = j+1; i< this.length; i++){
                    if( p_func(this[j], this[i]) > 0 ) { // 콜백함수로 오름차순/내림차순 제어 
                        var v_temp = this[j];
                        this[j] = this[i];
                        this[i] = v_temp;
                    }
            }
        }
        return this; 
        }
        alert(v_arr.mySort(function(a,b){
            return a - b; //오름차 
            return b - a; //내림차
        }));
</script>
```

#### 오늘의 문제(수정필요)
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    
    #id_center{
        position: relative;
        left:50px;
        top: -100px; /* 화면 밖에 숨기기 */
        width:100px;
        height:100px;
        font-size: 50px;
        text-align: center;  /* 수평 가운데 정렬*/
        line-height: 95px;  /* 글자 수직 가운데 정렬 */
        border:1px solid red;
    }

        .cl_layer1{
            position: absolute;
            left: 25px;
        }
        .cl_layer2{
            position: absolute;
            left: 125px;
        }
        .cl_layer3{
            position: absolute;
            left: 225px;
        }
        .cl_layer4{
            position: absolute;
            left: 325px;
        }
        .cl_layer5{
            position: absolute;
            left: 425px;
        }
        .cl_layer6{
            position: absolute;
            left: 525px;
        }
        
</style>
</head>
<body>
    <div id="id_center">
        <div id="id_first" class="cl_layer1"></div>
        <div id="id_second" class="cl_layer2"></div>
        <div id="id_third" class="cl_layer3"></div>
        <div id="id_fourth" class="cl_layer4"></div>
        <div id="id_fifth" class="cl_layer5"></div>
        <div id="id_sixth" class="cl_layer6"></div>
    </div>
    <input type=button value="클릭" id="id_btn">
    <script>
        
        var v_center = document.getElementById("id_center");
        var v_btn = document.getElementById("id_btn");

                var v_1 = document.getElementById("id_first");
                var v_2 = document.getElementById("id_second");
                var v_3 = document.getElementById("id_third");
                var v_4 = document.getElementById("id_fourth");
                var v_5 = document.getElementById("id_fifth");
                var v_6 = document.getElementById("id_sixth");


        function f_down(){
            if(!v_center.style.top){
                v_center.style.top = "-100px";
            }
            v_center.style.top = parseInt(v_center.style.top) + 10 + "px";
            if(parseInt(v_center.style.top) >= 300){
                return;
            }
            setTimeout(f_down,300);
        }

        var v_arr = new Array(7);
        
        //console.log(v_arr);
        //v_arr = Math.ceil((Math.random()*45)+1)
        v_btn.onclick = function(){
            f_down();
            var v_rslt = []; 
            for(var i=0; i< v_arr.length; i++){ 
                var v_isRepeat = false; 
                for(var j=0; j<v_rslt.length; j++){ 
                    if(v_rslt[j] == v_arr[i]){
                        v_isRepeat = true;
                        v_arr.push(Math.ceil(Math.random()*45));
                        break; 
                    }
                }
                
                if(!v_isRepeat){
                    v_rslt.push(v_arr[i]); 
                }
            }
            for(var j = 0; j < v_rslt.length; j++){
                for(var i = j+1; i< v_rslt.length; i++){
                    if(v_rslt[j] < v_rslt[i]){
                        var v_temp = v_rslt[j];
                        v_rslt[j] = v_rslt[i];
                        v_rslt[i] = v_temp;
                    }
                    
                }  
                
                
                
                
                // document.getElementById("id_first").innerHTML = v_rslt[1];
                // document.getElementById("id_second").innerHTML = v_rslt[2];
                // document.getElementById("id_third").innerHTML = v_rslt[3];
                // document.getElementById("id_fourth").innerHTML = v_rslt[4];
                // document.getElementById("id_fifth").innerHTML = v_rslt[5];
                // document.getElementById("id_sixth").innerHTML = v_rslt[6];
                
                //console.log(v_rslt[1]);
            }
            // function v_setTime(){
            // v_1.innerHTML = v_rslt[1];
            // v_2.innerHTML = v_rslt[2];
            // v_3.innerHTML = v_rslt[3];
            // v_4.innerHTML = v_rslt[4];
            // v_5.innerHTML = v_rslt[5];
            // v_6.innerHTML = v_rslt[6];

            // }


            for(i = 1; i <= 6; i++){
                    "v_"+i+".innerHTML= v_rslt["+i+"];"
                    return;
                    console.log(v_setTime);
                }

            // function v_setTime(){
            //     for(i = 1; i <= 6; i++){
            //         "v_"+i+".innerHTML= v_rslt["+i+"]";
            //         return;
            //         console.log(v_setTime);
            //     }
            // }
            // setTimeout(v_setTime,300);
            // }
            //v_setTime();

            }
    </script>
</body>
</html>
```
## 📚 15일차
#### 로또
```html
<!DOCTYPE html>
<meta charset="UTF-8">
<script>
    //중복체크 함수
    function f_isRepeat(p_arr,p_val){

        /*중복체크 함수(1)
        function f_isRepeat(p_arr, p_val){
            for(var i=0; i<p_arr.length; i++){
                if(p_arr[i]==p_val){
                    return true; // 배열 속에 p_val이 있으면 true 리턴 종료 
                }
            }
        }
        /*

        중복체크 함수(2)
        if(p_arr.indexOf(p_val) != -1){
            return true;
        }
        return false;
        */

       //중복체크 함수(3)
       return (p_arr.indexOf(p_val) != -1)? true:false;
    }


    //로또번호 생성 함수 
    function f_lotto(){
        var v_lottoNum = [];

        for(;"무한루프";){
            var v_ranNum = Math.ceil(Math.random()*45); //1~45
            if(!f_isRepeat(v_lottoNum, v_ranNum)){
                v_lottoNum.push(v_ranNum);
            }
            if(v_lottoNum.length == 6){
                break;
            }
            }
            return v_lottoNum.sort();
        }
        alert(f_lotto(function(a,b){
            return a-b;
        }));
</script>
```

#### 마우스오버
```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <table id="id_tbl1" border="2" width=400>
        <tr onmouseover="f_over(this)">
            <td>넘버</td>
            <td>이름</td>
            <td>별명</td>
        </tr>
        <tr onmouseover="f_over(this)">
            <td>1</td>
            <td>주영흔</td>
            <td>원자력</td>
        </tr>
        <tr onmouseover="f_over(this)">
            <td>2</td>
            <td>윤가영</td>
            <td>언니</td>
        </tr>
        <tr onmouseover="f_over(this)">
            <td>3</td>
            <td>장두언</td>
            <td>두마디</td>
        </tr>
        <tr onmouseover="f_over(this)">
            <td>4</td>
            <td>남기문</td>
            <td>기문둔갑</td>
        </tr>
    </table>
<script>
    //getElementsByTagName메소드는 일반적으로 잘 사용되지 않지만
    //xml문서를 다룰 때 사용됨 
    var v_tbl1 = document.getElementById("id_tbl1");
    var v_trs = v_tbl1.children[0].children; //table:tbody:tr
    var v_tr1 = v_tbl1.children[0].children[0]; // 

    

    function f_init(){
        for(var i=0; i<v_trs.length; i++){
            v_trs[i].style.backgroundColor="white";
            v_trs[i].style.color="black";
        }
    }
    
    
    function f_over(p_this){
        f_init();   //전체 초기화 
        p_this.style.backgroundColor="black";
        p_this.style.color="yellow";
    }

</script>
</body>
</html>
```


#### 마우스무브
```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    #container {
        width:95vw;
        height:95vh;
        border:1px solid black;
    }
    #id_nemo {
        position: absolute; /*기본값이 스태틱이라 다른 값을 줘야 움직임*/
        width:50px;
        height:50px;
        background-color: hotpink;
    }
</style>
</head>
<body>
<div id="container" onmousemove="f_mMv()">
    <div id="id_nemo"></div>
</div>    
<script>
    var v_nemo = document.getElementById("id_nemo");
    
    function f_mMv(){
        //마우스 좌표값 읽기
        console.log("X : " + event.clientX); // x좌표값
        console.log("Y : " + event.clientY); // y좌표값
        v_nemo.style.left = event.clientX + "px"; 
        v_nemo.style.top = event.clientY + "px"; 
    }
</script>
</body>
</html>
```

#### 이벤트 주의1
```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            border:3px solid gold;
        }
    </style>
</head>
<body>
<div style="width:400px;height:400px;position: relative;left:100px" onmouseover="f_check2()">
    김주헌 할머닝
    <div style="width:200px;height:200px" onmouseover="f_check1()">
        정찬웅 어머닝
        <div style="width:100px;height:100px" onmouseover="f_check()">
            황미선 딸
        </div>
    </div>
</div>
<script>
    function f_check(){
        // 부모에게 이벤트가 전달되는 것을 이벤트 버블링이라고 부름
        // 아주 기분 나쁨
        event.stopPropagation();  // 꼭 기억, 아주 중요
        alert("나 황미선");
    }
    function f_check1(){
        event.stopPropagation();  // 꼭 기억, 아주 중요
        alert("나 정찬웅");
    }
    function f_check2(){
        event.stopPropagation();  // 꼭 기억, 아주 중요
        alert("나 김주헌");
    }
</script>    
</body>
</html>
```

#### 이벤트 주의2
```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- 아래 처럼 쓰지 맙시당
        <a href="javascript:f_ck2()" onclick="f_ck()">다음</a>
    -->
    <a href="http://daum.net" onclick="f_ck()">다음</a>
<script>
    function f_ck2(){
        alert("난 href");
    }
    function f_ck(){
        event.preventDefault(); // 디폴트 이벤트 막기, 여기선 a태그의 링크기능을 막음
       // event.stopPropagation(); // 이벤트 전파 막기, (이벤트 캡처링)
        alert("눌렀니?");
    }
</script>    
</body>
</html>
```

#### this에 대해
```html
<!DOCTYPE html>
<meta charset="UTF-8">
<script>
    //this? -> 나
//window.alert(this);//? window?
/*
function f_ck(){
    alert(this);//? 
}    
window.f_ck();
*/
/* javascript의 this는 개발자의 불만을 하늘높이 올려서 열받게 만듬
var v_obj = {};  // 빈객체 생성
v_obj.name="나 v_obj얌"
v_obj.print = function(){ // 메소드 추가
    alert(this.name); //?
    return;
}
//v_obj.print();
var v_trick = v_obj.print;
window.v_obj.print();
//alert("결과:" + v_trick);
*/
// this의 사용이 애매해서 개발자가 직접 this 값을 세팅해서 쓸수 있도록
// 3개의 메소드가 출현, call, apply, bind  -> bind는 좀더 특별

var v_obj = {};  // 빈객체 생성
v_obj.name="윤가영언니";

function f_call(p_arg1,p_arg2){
    alert(this.name + p_arg1 + p_arg2);
}
//f_call(); // this -> window
// call 하고 apply는 매개변수 넘기는 방식만 다르므로, 둘중 하나를 선택하면
// 일관성 있게 사용하는 것이 좋음
//f_call.call(v_obj,"  첫번째 매개변수 ", " 두번째 매개변수 ");
//f_call.apply(v_obj,["  첫번째 ", " 두번째 "]);

// f_call.bind(v_obj)("헤헤헤","히히히");
// f_call.bind(v_obj,"헤헤헤","히히히")();
var v_newFunc = f_call.bind(v_obj,"헤헤헤","히히히");
v_newFunc();

var System = {};
System.out = {};
/*
System.out.print = function(p_msg){
    document.write(p_msg);
}
*/
System.out.print = document.write.bind(document);
System.out.print("<h1>난 최고의 프로그래머 오성현이당</h1>");

//var myPrint = document.write;


 // bind는 내부적으로 새로운 함수를 만들어서 함수를 리턴(함수포인터)해 줌
</script>

```

#### 오늘의 과제(태양계) - 수정필요
```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #id_earth{
            position: absolute;
            border-radius: 25px;
        }
        #id_sun{
            position: absolute;
            border-radius: 50px;
        }
        #id_moon{
            position: absolute;
            border-radius: 50px;
        }
    </style>
</head>
<body>
    <img id="id_sun" src="./img/sun.jpg" width="100" height="100">
    <img id="id_earth" src="./img/earth.png" width="50" height="50">
    <img id="id_moon" src="./img/moon.jpg" width="50" height="50">
<script>
    var v_sun = document.getElementById("id_sun"); 
    var v_earth = document.getElementById("id_earth"); 
    var v_moon = document.getElementById("id_moon"); 
    var v_sunGak = 0;
    //태양 제자리에서 돌리기

    function f_sunRotate(){
        v_sunGak = (v_sunGak + 10) % 360; 
        v_sun.style.transform = "rotate("+ v_sunGak +"deg)";
        setTimeout(f_sunRotate,10);
    }
    //지구 돌리기 
    var v_Radius = 150;
    var v_earGak = 0;  
    var v_moonGak = 0;

    function f_earthRotate(){
        v_earGak = (v_earGak + 5) % 360;
        v_earth.style.left = (v_centerX-25) + v_Radius *Math.cos(v_earGak*Math.PI/180) + "px";
        v_earth.style.top = (v_centerY-25) + v_Radius *Math.sin(v_earGak*Math.PI/180) + "px";
        setTimeout(f_earthRotate,25); 
    }

    function f_moonRotate(){
        v_moonGak = (v_moonGak + 5) % 360;
        v_moon.style.left = (v_centerX-200) + v_Radius *Math.cos(v_moonGak*Math.PI/180) + "px";
        v_moon.style.top = (v_centerY-200) + v_Radius *Math.sin(v_moonGak*Math.PI/180) + "px";
        setTimeout(f_moonRotate,25); 
    }

    //초기화 
    var v_centerX;//화면 중심x
    var v_centerY;//화면 중심y
    window.onload = function(){
        v_centerX = window.innerWidth /2;
        v_centerY = window.innerHeight /2;
        v_sun.style.left = (window.innerWidth - 100)/2 + "px";
        v_sun.style.top = (window.innerHeight - 100)/2 + "px"; 
        f_sunRotate();
        f_earthRotate(); 
        f_moonRotate();
    }
    //윈도우 사이즈 변경시 자동으로 기준점 변경 
    window.onresize = function(){
        v_centerX = window.innerWidth /2;
        v_centerY = window.innerHeight /2;
        v_sun.style.left = (window.innerWidth - 100)/2 + "px";
        v_sun.style.top = (window.innerHeight - 100)/2 + "px"; 
    }
</script>
</body>
</html>
```

## 📚 16일차
#### 이벤트 버블링 방지 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
    #id_hal{
        width: 200px;
        height: 200px;
        border: 1px solid black;
    }

    #id_mom{
        width: 100px;
        height: 100px;
        border: 1px solid black;
    }

    #id_me{
        width: 50px;
        height: 50px;
        border: 1px solid black;
    }
    </style>

</head>
<body>
    <div id="id_hal" onclick="f_hal()">할머니
        <div id="id_mom" onclick="f_mom()">엄마
            <div id="id_me" onclick="f_me()">
                사승원
            </div>
        </div>
    </div>

    <script>
        function f_hal(){
            alert("나 할머니");
        }


        function f_mom(){
            alert("나 엄마");
            //이벤트버블링 나오면 안 좋음 
        }


        function f_me(){
            event.stopPropagation(); 
            //event.stopPropagation 이벤트버블링 막아줌
            alert("나 나");

        }

    </script>
</body>
</html>
```

#### 마우스로 도형 끌기 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    #container {
        width:95vw;
        height:95vh;
        border : 1px solid black;
    }
    #id_nemo {
        position: absolute;
        width:100px;
        height:100px;
        background-color:pink;
    }
</style>
</head>
<body>
    <div id="container">
        <div style="left: 10px;top:10px" id="id_nemo" onmousedown="f_mDown()" 
                                                      onmouseup="f_mUp()" 
                                                      onmousemove="f_mMove()"
                                                      onmouseout="f_mOut()">
        </div>
    </div>    
<script>
    //마우스 왼쪽 버튼을 누른 상태로 움직이면 id_nemo도 같이 움직이도록
    //마우스 좌표 event.clientX, event.clientY

    //마우스 왼쪽버튼 누른 상태로 움직이면 id_nemo도 같이 움직이도록 하기 
    var v_isLeftPressed = false;
    var v_nemo = document.getElementById("id_nemo");
    var v_msX;  //마우스 X
    var v_msY;  //마우스 Y
    var v_nemoX;//네모 X
    var v_nemoY;//네모 Y

    function f_mDown(){
        console.log("마우스 버튼 누름");
        if(event.button == 0){
            v_msX = event.clientX
            v_msY = event.clientY
            v_nemoX = parseInt(v_nemo.style.left);
            v_nemoY = parseInt(v_nemo.style.top);
            v_isLeftPressed=true;
        }
    }


    function f_mUp(){
        console.log("마우스 버튼 놓았닝?");
        v_isLeftPressed = false;
    }


    function f_mMove(){
        if(v_isLeftPressed){
            v_nemo.style.left = v_nemoX + (event.clientX - v_msX) + "px"; 
            v_nemo.style.top = v_nemoY + (event.clientY - v_msY) + "px"; 

        }
    }

    function f_mOut(){
        v_isLeftPressed = false; 
    }

</script>
</body>
</html>
```

#### 마우스 오른쪽 버튼 막기
```html
<!DOCTYPE html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    #wrapper {
        width:95vw;
        height:95vh;
        border:3px dashed black;
        border-style:dotted;
    }
</style>
</head>
<body>
<div id="wrapper" onmousedown="f_mDown()"></div>
<script>
    function aaa(){
    }
    //함수는 true다 왜 객체라서
    if(aaa){
        alert("사승원"); //?
    }

    document.getElementById("wrapper").oncontextmenu = function(){
        event.preventDefault();
        event.stopPropagation();
    }

    /*
    document.getElementById("wrapper").addEventListener("contextmenu",function(){
        //return false; //?
        event.preventDefault();
        event.stopPropagation();
    });
    */


    //context menu, 별도 이벤트
    function f_mDown(){
        if(event.button == 2){
            alert("오른쪽 누르지 마세요");
        }
    }
   
   /* 이벤트 등록법 3가지
     1. 태그에 직접 기술 
     2. 요소의 on이벤트명 속성이용
     3. addEventListener 메소드 이용  (권장방식)
   */

  /* 이벤트 등록법 2번은 같은 이벤트를 기술하면 덮어써버림, 나중것만 실행됨
  window.onload = function(){
      alert("자동 페이지로딩이 끝나면 실행됨!");
  }

  window.onload = function(){
      alert("저도 실해되나요?");
  }
  */

  /* 3번은 덮어쓰지 않고 내부의 이벤트 큐(Queue)라고 곳에 등록되서 순서대로 사용됨*/
  window.addEventListener("load",function(){
    alert("난 권장방식 3번이야");
  });

  window.addEventListener("load",function(){
    alert("나도 권장방식 3번을 썼는데 어떻게 되지?");
  });

    


</script> 
</body>
</html>
```

#### 파일 타입에 이미지 넣기
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #id_disp{
            width: 200px;
            height: 200px;
            border: 1px solid black;
        }
    </style>
</head>
<body>
    <!-- 거의 항상 이런 식으로 밖에 쓰이질 않으니 이걸 계속 활용하면 됨 -->
    <div id="id_disp"></div>
    <input id="id_file" type="file" value="" accept=".jpg,.jpeg,.png,.gif">
    <!-- accept : 확장자를 제한할 수 있음 -->
    <script>
        var v_selfile = document.getElementById("id_file");
        var v_disp = document.getElementById("id_disp");

        v_selfile.onchange = function(){
            console.log(v_selfile.files); // files는 파일을 가지고 있는 배열로 봐도 무방하다
            var v_file = v_selfile.files[0]; 
            var v_fileReader = new FileReader(); // FileReader : 파일을 읽어주는 사람이 필요 
            v_fileReader.readAsDataURL(v_file); // readAsDataURL : 제일 많이 사용 
            v_fileReader.onload = function(){   // onload : 파일리더가 다 읽었다고 알려주는 이벤트 
                console.log(v_fileReader.result); // 읽은 내용을 result에 저장시킴 
                v_disp.innerHTML=""; //사진 하나만 넣어야하니까 먼저 비우고 
                var v_img = document.createElement("img");  
                v_img.setAttribute("src",v_fileReader.result); // 이미지 내용 할당
                v_img.setAttribute("width",200);
                v_img.setAttribute("height",200);
                v_disp.appendChild(v_img);
            }
        }
    </script>
</body>
</html>
```

#### 사진 앨범 만들기(createElement(""))
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #id_disp{
            width: 300px;
            height: 300px;
            border:1px solid black;
            overflow: hidden;
        }
        #id_acja{
            width: 1800px;
            height: 1800px;
        }
    </style>
</head>
<body>
    <div id="id_disp">
        <div id="id_acja"></div>
    </div>
    <input id="id_btn" type="button" value="사승원123">
    <input type="button" value="누르세요" id="id_btn2">

    <script>
        var v_disp = document.getElementById("id_disp");
        var v_acja = document.getElementById("id_acja");
        var v_btn = document.getElementById("id_btn");
        var v_btn2 = document.getElementById("id_btn2");
        v_btn2.addEventListener("click",function(){
            //이미 존재하는 객체를 붙여 넣으면 맨뒤에 가서 붙음
            //appendChild를 잘 활용하면 사진 돌게 할 수 있음 
            v_acja.appendChild(v_acja.children[0]);
        });


    var v_index = 1; 
    
    function f_click(){
        // //DOM(Document Object Model) 객체 생성하기 
        /*
        테이블의 경우는 이렇게 넣어도 되긴 하지만 소스가 많이 길어져서
        보통은 그냥 문자열 더하기로 넣는다. 
        */

        // var v_table = document.createElement("table");
        // v_table.border="2";
        // var v_tr = document.createElement("tr"); 
        // var v_td = document.createElement("td");
        // v_td.innerHTML="td의 값";

        // v_tr.appendChild(v_td);
        // v_table.appendChild(v_tr);
        // v_disp.appendChild(v_table);


        // var v_atag = document.createElement("a");
        // v_atag.href="./img/son3.jepg";
        // v_atag.innerHTML = "이너HTML"
        // v_disp.appendChild(v_atag); 

        var v_img = document.createElement("img"); //img 태그 객체 생성(메모리 상에)
        v_img.setAttribute("src","./img/son"+v_index+".jpeg");
        v_img.setAttribute("width","300");
        v_img.setAttribute("height","300");
        //alert(v_img.getAttribute("src")); 
        //v_img.src="./img/son" + v_index + ".jpeg";
        //v_img.width=300;
        //v_img.height=300;
        //v_disp.append //기능은 더 많으나 브라우져 호환성에 문제가 있으니까 사용 자제 
        v_acja.appendChild(v_img); //눈에 보이게 
        v_index++;
    }
    v_btn.addEventListener("click", f_click);
</script>
</body>
</html>

```

#### 오늘의 문제(로또번호 내려오게 하기) - 수정필요
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #id_back{
            width: 300px;
            height: 300px;
            background-color: chocolate;
        }
        .cl_data{
            display: inline-block;
            border: 1px solid black;
            
        }
        

    </style>
    
</head>
<body>
    <div id="id_back">
        <div id="id_data0" class="cl_data">1</div>
        <div id="id_data1" class="cl_data">2</div>
        <div id="id_data2" class="cl_data">3</div>
        <div id="id_data3" class="cl_data">4</div>
        <div id="id_data4" class="cl_data">5</div>
        <div id="id_data5" class="cl_data">6</div>
        <div id="id_data6" class="cl_data">7</div>
        <div id="id_data7" class="cl_data">8</div>
        <div id="id_data8" class="cl_data">9</div>
    </div>
    
    <script>
        var v_datas = [80,100,56,120,180,30,40,120,160];
        var v_height = document.createElement("height"); 

        document.getElementById("id_data0").innerHTML =  v_datas[0];
        v_height.setAttribute("height", v_datas[0]);
         


    </script>
</body>
</html>
```

## 📚 17일차
#### 드래그앤드롭 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    #id_disp {
        width:300px;
        height:300px;
        border:2px solid black;
    }
</style>
</head>
<body>
    <!-- 드래그앤 드랍도 거의 요렇게 밖에 안 쓰이니, 이 파일을 잘 보관합니다 -->
    <div id="id_disp" ondragover="f_mDragOver()" ondrop="f_mDrop()">
        사진올려주세요
    </div>
<script>
    var v_disp = document.getElementById("id_disp");
    function f_mDragOver(){
        event.preventDefault();
    }
    function f_mDrop(){
        event.preventDefault();
        //console.log(event.dataTransfer.files);
        var v_file = event.dataTransfer.files[0];
        var v_fileReader = new FileReader();
        v_fileReader.readAsDataURL(v_file);
        v_fileReader.onload = function(){
            var v_img = document.createElement("img");
            v_img.src = v_fileReader.result; 
            v_img.width=100;
            v_img.height=100;
            v_disp.appendChild(v_img);
        }

    }

    window.addEventListener("dragover",function(){
        event.preventDefault();
    });
    window.addEventListener("drop",function(){
        event.preventDefault();
    });
</script>
</body>
</html>
```

#### cssClass
```html 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    .ngm {
        height: 100px;
        background-color: green;
    }
    .ksm {
        height: 100px;
        background-color: yellow;
    }
    .fgColor{
        color: blue;
    }
</style>
</head>
<body
    <div id="id_disp"></div>
<script>
    /* class는 자바스크립트 키워드 setAttribute 사용권장, 문자열 더하기 주의 */
    //document.getElementById("id_disp").class = "ksm";
    document.getElementById("id_disp").setAttribute("class","ksm fgcolor");
    //document.getElementById("id_disp").className = "ksm";
    //document.getElementById("id_disp").className = "fgColor";
    // document.getElementById("id_disp").className = "ksm";
    // document.getElementById("id_disp").className = 
    //     document.getElementById("id_disp").className + "fgColor";
</script>
</body>
</html>
```

#### 플리커
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script>
        var v_imgURLS;
        function jsonFlickrFeed(p_data){
            /*
            v_imgURLS = [];
            for(var i=0; i< p_data.items.length; i++){
                console.log(p_data.items[0].media.m);
                v_imgURLS.push(p_data.items[i].media.m);
            }
            */
           // alert(v_imgURLS);
           console.log("불리는지 단순 체크용 ");
           for(var i=0; i< p_data.items.length; i++){
                var v_img = document.createElement("img"); // 이미지 태그(객체)생성
                v_img.src = p_data.items[i].media.m;
                v_disp.appendChild(v_img);
            }
        }
    </script>
    <title>Document</title>
</head>
<body>
    이미지검색어<input id="id_txt" type=text value="">
    <input type=button value="검색" id="id_imgIn">
    <div id="id_disp"></div>
    <script>
        var v_disp = document.getElementById("id_disp");
        var v_imgIn = document.getElementById("id_imgIn");
        var v_txt = document.getElementById("id_txt");
        var v_preURL = "https://www.flickr.com/services/feeds/photos_public.gne?tags=";
        var v_postURL = "&format=json";
        v_imgIn.addEventListener("click",function(){
            var v_totalURL = v_preURL + v_txt.value + v_postURL;
            var v_script = document.createElement("script");
            v_script.src = v_totalURL;
            document.head.appendChild(v_script);
        });
        /*
        v_imgIn.addEventListener("click",function(){
            for(var i=0; i< v_imgURLS.length; i++){
                var v_img = document.createElement("img"); // 이미지 태그(객체)생성
                v_img.src = v_imgURLS[i];
                v_disp.appendChild(v_img);
            }
        });
        */
    </script>
</body>
</html>
```

#### 플리커2
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- 정리된 소스 -->
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script>
        /*
          JSONP -> JSON PADDING
        */
        function jsonFlickrFeed(p_data){
           console.log("함수가 불리는지 단순 체크용 ");
           console.log(p_data);
           v_disp.innerHTML = ""; // 기존 것 지우기
           for(var i=0; i< p_data.items.length; i++){
                var v_img = document.createElement("img"); // 이미지 태그(객체)생성
                v_img.src = p_data.items[i].media.m;
                v_disp.appendChild(v_img);
            }
        }
    </script>
    <title>이미지검색</title>
</head>
<body>
    이미지검색어<input id="id_txt" type=text value="">
    <input type=button value="검색" id="id_imgIn">
    <div id="id_disp"></div>
    <script>
        var v_disp = document.getElementById("id_disp");
        var v_imgIn = document.getElementById("id_imgIn");
        var v_txt = document.getElementById("id_txt");
        var v_preURL = "https://www.flickr.com/services/feeds/photos_public.gne?tags=";
        var v_postURL = "&format=json";
        v_imgIn.addEventListener("click",function(){
            if(document.getElementById("flickr")){
                document.head.removeChild(document.getElementById("flickr"));
            }
            var v_totalURL = v_preURL + v_txt.value + v_postURL;
            var v_script = document.createElement("script");
            v_script.setAttribute("id","flickr");
            v_script.src = v_totalURL;
            document.head.appendChild(v_script);
        });
    </script>
</body>
</html>
```

#### 오늘의 문제 - 수정필요
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    #id_disp {
        width:300px;
        height:300px;
        border:2px solid black;
    }
</style>
</head>
<body>
    <!-- 드래그앤 드랍도 거의 요렇게 밖에 안 쓰이니, 이 파일을 잘 보관합니다 -->
    <div id="id_disp" ondragover="f_mDragOver()" ondrop="f_mDrop()">
        사진올려주세요
    </div>
<script>
    var v_disp = document.getElementById("id_disp");
    function f_mDragOver(){
        event.preventDefault();
    }
    function f_mDrop(){
        event.preventDefault();
        //console.log(event.dataTransfer.files);
        var v_file = event.dataTransfer.files[0];
        var v_fileReader = new FileReader();
        v_fileReader.readAsDataURL(v_file);
        v_fileReader.onload = function(){
            var v_img = document.createElement("img");
            v_img.src = v_fileReader.result; 
            v_img.width=100;
            v_img.height=100;
            v_disp.appendChild(v_img);
        }

    }

    window.addEventListener("dragover",function(){
        event.preventDefault();
    });
    window.addEventListener("drop",function(){
        event.preventDefault();
    });

    //오늘의 과제 : 파일 여러 개 끌어다 놓았을 때 끌어온 파일 모두 넣기 
</script>
</body>
</html>
```
## 📚 18일차
#### 드래그앤드랍2
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    #id_disp {
        width:300px;
        height:300px;
        border:2px solid black;
    }
</style>
</head>
<body>
    <!-- 드래그앤 드랍도 거의 요렇게 밖에 안 쓰이니, 이 파일을 잘 보관합니다 -->
    <div id="id_disp" ondragover="f_mDragOver()" ondrop="f_mDrop()">
        사진올려주세요
    </div>
<script>
    var v_disp = document.getElementById("id_disp");
    function f_mDragOver(){
        event.preventDefault();
    }

    /*
       반복문 안에 비동기방식 코드가 있을 때는 
       코드를 별도 함수(함수도 객체이기 때문에)로 뺀당, 기억합시당 꼭
    */

    function f_readFile(p_file){
        var v_fileReader = new FileReader();
        v_fileReader.readAsDataURL(p_file);
        v_fileReader.onload = function(){
            var v_img = document.createElement("img");
            v_img.src = v_fileReader.result; 
            v_img.width=100;
            v_img.height=100;
            v_disp.appendChild(v_img);
        }
    }

    function f_mDrop(){
        event.preventDefault();
        //console.log(event.dataTransfer.files);
        // 파일 1개만 끌어다 놓았을 때
        var v_files = event.dataTransfer.files; 
        for(var i=0; i< v_files.length; i++){
            f_readFile(v_files[i]);
        //alert(v_fileReader.result);  // 힌트, 비동기
        }

        
       /* 오늘의 과제 파일 여러개 끌어다 놓았을 때
          끌어온 파일 모두 넣기 
       */

    }

    window.addEventListener("dragover",function(){
        event.preventDefault();
    });
    window.addEventListener("drop",function(){
        event.preventDefault();
    });
</script>
</body>
</html>
```

#### tableindex
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- 정리! 
        tableindex는 tab 눌렀을 때 focus 가는 순서 지정
        tabindex = -1 : focus 안 가도록 설정
        tabindex = 0 : focus 받을 수 없는 element(요소)가 focus 받을 수 있도록 설정-->
    아이디 <input tabindex="1" type="text" value="" autofocus><br>
    암호 <input tabindex="3" type="password" value="" ><br>
    별명 <input tabindex="-1s" type="text" value=""><br>
    이메일 <input tabindex="2" type="text" value=""><br>
    주소 <input tabindex="5" type="text" value=""><br>

</body>
</html>
```

#### location객체(href속성, replace 메소드 , reload)
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- download : 이미지 다운로드 해줌 -->
    <a href="./img/son5.jpeg" download="son1.jpeg">손</a><br>
    <a id="id_check" href="./img/pool1.jpeg" onclick="f_download(this)">풀 다운로드</a><br>
    <input type="button" value="풀 다운로드" onclick="f_download()">
    <!-- 링크이동은 a태그로 -->
    <input type="button" value="이동" onclick="f_mv()">
    <script>
        function f_download(){
            //event.preventDefault();// a태그의 링크 기능(기본기능) 막기
            document.getElementById("id_check").download = "pool1.jpeg";
            document.getElementById("id_check").click(); 
                   }

        function f_mv(){
            //주소표시줄을 의미하는 location객체 
            //location에서 기억해야할 세 가지
            //href속성, replace 메소드 , reload(잘 안 씀)
            //alert(window.location.href);

            /*
                href 속성 vs replace 메소드
                href는 캐쉬를 사용
                replace는 서버에 다시 요청
            */

            //location.href = "http://mail3.nextit.or.kr";
            //location.replace("http://mail3.nextit.or.kr"); //변경된 내용을 가져와야할 때 사용
            //location.reload(); // 현재 페이지 다시 로딩, 새로고침 버튼 누른 효과(별로 좋지 않음)
        }
    </script>
</body>
</html>
```

#### 특별한 반복문(for-in)
```html
<!DOCTYPE html>
    
<meta charset="UTF-8">
<script>
    //특별한 반목문 for(var 변수명 in 객체)
    var v_arr = ["영", "일", "이"];
    v_arr.splice(1,1); //배열의 특정 값을 삭제(중요!!) 
    alert(v_arr); // 지워졌는지 확인 

    var v_obj = {}; 
    v_obj.name = "사승원";
    v_obj.age = 26;
    //객체 속성 지우기
    delete v_obj.name; // 많이 사용하지는 않는다. 

    for(var v_atr in v_obj){
        alert(v_atr); 
    }
    /*
    for(var v_one in v_arr){
        alert(v_one + "   " + v_arr[v_one]);// 0,1,2 -> 배열의 index값 알림 
    }
    */

    /*
   var v_obj = {
       "attr1" : "속성1",
       "attr2" : "속성2",
       "attr3" : "속성3",
       "attr4" : "속성4",
       "attr5" : "속성5"
   };
   */
  //위의 것과 똑같은 걸 쉽게 for문으로 만들기
   var v_obj = {};
   for(var i=1; i<=5; i++){
       v_obj["attr"+i] = "속성" +i;
   }



   //속성 명 말고 속성 값 불러오고 싶을 때 
   //alert(v_obj["attr1"]); //엄청 중요!!

   for(var v_attr in v_obj){
       //alert(v_attr + " " + v_obj.attr); 이건 안 됨 
       alert(v_attr + " " + v_obj[v_attr]); //중요!!!!!!
   }

   for(var v_ssw  in window){
        document.write(v_ssw + " " + document[v_ssw] + "<br>"); 
   }
</script>
```

#### 키보드이벤트1
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- 주로 쓰는 키보드이벤트 keypress, keydown -->
    <!-- <input type="text" value="" onkeydown="f_key()"> -->
주민번호<input type="text" id="id_txt1" value="" onkeypress="f_key()">-
       <input type="text" id="id_txt2" value="">
<script>
    /*
    keypress : 어떤 글자를 눌렀는지 구분하기 위한 이벤트
    keydown  : 어떤 버튼을 눌렀는지 구분하기 위한 이벤트 -> 더 많이 사용됨
    */
   var v_txt1 = document.getElementById("id_txt1");
   var v_txt2 = document.getElementById("id_txt2"); 

    function f_key(){
        /*
        if(event.keyCode == "13");//엔터의 키코드가 13
            v_txt2.focus(); 
            //엔터키를 치면 커서를 v_txt2로 올겨라(focus 메소드도 자주 사용되는 메소드임)
        */
        
        if(v_txt1.value.length == 5){
            v_txt2.focus();
        }
    }

</script>
</body>
</html>
```

#### 키보드이벤트2
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #id_back{
            position: relative;
            width: 300px;
            height: 400px;
            border: 2px solid black;
        }
        #id_bar{
            position: absolute;
            overflow: hidden;
            width: 100px;
            height: 25px;
            bottom: 40px;
            background-color: blueviolet;
            
        }
    </style>
</head>
<body>
    <div id="id_back" tabindex="0" onkeydown="f_kDown()">
        <div id="id_bar"></div>
    </div>
    <script>
        var v_bar = document.getElementById("id_bar");

        if(!v_bar.style.left){
            v_bar.style.left = "30px"; 
        }

        var v_mvWidth=10;
        function f_kDown(){
            if(event.keyCode == "37"){ //왼쪽 화살표 : 37 오른쪽 화살표 : 39
                if(parseInt(v_bar.style.left)<=0){
                    return;
                }
                v_bar.style.left = parseInt(v_bar.style.left) - v_mvWidth + "px"; 
            }
            if(event.keyCode == "39"){
                var v_right  = parseInt(v_bar.style.left) + 100;
                if(v_right >= 300){
                    return; // 아무 일도 안 하기

                }
                v_bar.style.left = parseInt(v_bar.style.left) + v_mvWidth + "px"; 
            }
        }
    </script>
</body>
</html>
```

#### 오늘의 문제(갤러그) - 수정필요
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #id_back{
            position: relative;
            width: 300px;
            height: 400px;
            border: 2px solid black;
        }

        #id_ball{
            position: absolute;
            width: 50px;
            height: 50px;
            background-color: chartreuse;
            top: 150px;
            left: 100px;

            border-radius: 50px; 
            background-image: url("./img/dog3.jpeg");
            background-size: 50px 50px;
        }

        #id_bar{
            position: absolute;
            overflow: hidden;
            width: 100px;
            height: 25px;
            bottom: 40px;
            background-color: blueviolet;
            
        }
    </style>
</head>
<body>
    <div id="id_back" tabindex="0" onkeydown="f_kDown()">
        <div id="id_bar"></div>
        <div id="id_ball"></div>
    </div>
    <input type="button" value="오른쪽으로 가기" onclick="f_cont()">
    <input type="button" value="그만가" onclick="f_stop()">

    <script>
        var v_mvR = 10; 
        var v_mvT = 10; 
        var v_bar = document.getElementById("id_bar");
        var v_timer;
        var v_run = false;


        function f_cont(){
            if(!v_run){
            f_move();
            v_run = true;
            }
        }
        // 바 움직이기
        if(!v_bar.style.left){
            v_bar.style.left = "30px"; 
        }
        
        var v_mvWidth=10;

        function f_kDown(){
            if(event.keyCode == "37"){ //왼쪽 화살표 : 37 오른쪽 화살표 : 39
                if(parseInt(v_bar.style.left)<=0){
                    return;
                }
                v_bar.style.left = parseInt(v_bar.style.left) - v_mvWidth + "px"; 
            }
            if(event.keyCode == "39"){
                //alert(v_bar.style);
                var v_right  = parseInt(v_bar.style.left) + 100;
                if(v_right >= 300){
                    return; // 아무 일도 안 하기
                    
                }
                v_bar.style.left = parseInt(v_bar.style.left) + v_mvWidth + "px"; 
            }
        }

        
        
        var v_mvR = 10; /* 움직이는 폭 */ 
        var v_mvT = 10; /* 움직이는 상하 */
        var v_timer; 
        var v_ball = document.getElementById("id_ball");

        
        //버튼 누르면 속도 빨라지는 거 안 되게 한 번만 실행할 수 있게 해주기
        //직접 가는 걸 중간에 한 번 거쳐서 조건을 줘서 제어가능(proxy 패턴)
        var v_run = false;
        function f_cont(){
            if(!v_run){
                f_move();
                v_run = true;

            }
        }
        
        //멈추기 
        function f_stop(){
            clearTimeout(v_timer);
            v_run =false;
        }
        
        //움직이기
        function f_move(){
            if(!v_ball.style.left){/* 원래 빈공백인데 !로 '만약 정의되지 않았다면?'*/
            v_ball.style.left = "100px"; /* 초기값을 100px로 정의할 수 있음 단위값(px)를 꼭 줘야함*/
            v_ball.style.top = "150px";
            }
            v_ball.style.transform = "skewX(0deg) skewY(0deg)"
            v_ball.style.left = parseInt(v_ball.style.left) + v_mvR + "px";
            v_ball.style.top = parseInt(v_ball.style.top) + v_mvT + "px";
            
            var v_left = parseInt(v_ball.style.left);
            var v_right = parseInt(v_ball.style.left)+ 100;
            var v_top = parseInt(v_ball.style.top) ;
            var v_bottom = v_top + 100; 
        
            
            if(v_right >= 350 || v_left <=0){// 좌우충돌
                v_ball.style.transform = "skewY(45deg)"
                v_mvR = -v_mvR;
            }
            
            if(v_bottom >= 380 || v_top <=0){//방향 바꾸기 
                v_ball.style.transform = "skewX(45deg)"
                v_mvT = -v_mvT;
            }
            
            v_timer = setTimeout(f_move,50);//0.05초마다 버튼 누르면 자동으로 오른쪽으로 움직임
        }
        
        
        </script>
</body>
</html>
```
## 📚 19일차
#### 어제 문제 정답
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    #id_back {
        position: relative;
        overflow: hidden;
        width:300px;
        height:400px;
        border:2px solid black;
    }
    #id_bar {
        position: absolute;
        width:100px;
        height:25px;
        top: 340px;
        background-color: hotpink;
    }
    #id_ball {
        position: absolute;
        width:50px;
        height:50px;
        background-color: gold;
        border-radius: 25px;
    }
</style>
</head>
<body>
    <input type=button value="씨짝" onclick="f_mv()">
    <div id="id_back"  tabindex="0" onkeydown="f_kDown()">
        <div id="id_ball"></div>
        <div id="id_bar"></div>
    </div> 
<script>
    var v_ball = document.getElementById("id_ball");
    v_ball.style.left = Math.round(Math.random()*250) + "px";
    v_ball.style.top = Math.round(Math.random()*20) + "px";
    var v_mvW = 10;
    var v_mvH = 10;
    function f_mv(){
        v_ball.style.left = parseInt(v_ball.style.left) + v_mvW + "px";
        v_ball.style.top = parseInt(v_ball.style.top) + v_mvH + "px";
        var v_left = parseInt(v_ball.style.left);
        var v_top = parseInt(v_ball.style.top);
        var v_right = v_left + 50;
        var v_bottom = v_top + 50;
        //막대 충돌
        var v_btmmCheck = (v_bottom >= 340);
        var v_leftCheck = (v_right >= parseInt(v_bar.style.left));
        var v_rightCheck = (v_left <= parseInt(v_bar.style.left)+100); 
        if(v_btmmCheck && v_leftCheck && v_rightCheck){
            v_mvH = -v_mvH;
        }



        //벽충돌
        if(v_left <= 0 || v_right >= 300){
            v_mvW = - v_mvW;
        }
        if(v_top <=0 || v_bottom >= 400){
            v_mvH = -v_mvH;
        }
        setTimeout(f_mv,200);
    }


    var v_bar = document.getElementById("id_bar");
    if(!v_bar.style.left){
        v_bar.style.left = "30px";
    }
    var v_mvWidth=10;
    function f_kDown(){
        if(event.keyCode == "37"){  // 왼쪽화살표 37, 오른쪽 39번
            if(parseInt(v_bar.style.left)<=0){
                return;
            }
            v_bar.style.left = parseInt(v_bar.style.left) - v_mvWidth + "px";
        }
        if(event.keyCode == "39"){
            var v_right = parseInt(v_bar.style.left) + 100;
            if(v_right >= 300){
                return;            // 아무일도 안하깅
            }
            v_bar.style.left = parseInt(v_bar.style.left) + v_mvWidth + "px";
        }
    }


</script>     
</body>
</html>
```

#### form
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- 
        서버로 뭔가 전송하려면 꼭 form 태그로 둘러싸야 한다.
        서버로 정보를 보내려는 입력태그에는 꼭 name속성이 있어야 한다. 
        ? 뒤에 문자열 전체를 QueryString(쿼리스트링)이라고 한다

        쿼리스트링이 보이는 전송방식을 get방식이라고 부름(default값)<form action="" method="get">
        쿼리스트링이 안 보이는 전송 방식을 post 방식이라고 부름 (<form action="" method="POST">)
        기본적으로 개발자가 get방식 상태에서 개발해야 디버깅이 편해서 생산성이 높아짐 
        민감한 정보는 확인해서 post방식으로 바꿔야 함 

        action의 default값은 자기 자신

        form 태그의 onsubmit 이벤트는 전송 직전에 발생한다.(true : 전송됨/false : 전송안됨)
        required : 이 입력란을 작성하세요 문구 알림(submit 버튼이 있을 때만 동작) 
        onsubmit="return f_submit()"

        page에 form 태그는 여러 번 들어가도 상관없음
        하지만 form안에 form을 넣진 않음
     -->
    <form id="id_form" action="인코딩.html" method="get" >
        아이디 <input type="text" id="id_id" name="nm_id" value="" required><br>
        별명 <input type="text" name="nm_alias" value="" required><br>
        <input type="submit" value="전달">
        <input type="reset" value="맨처음값으로">
    </form>
    <hr>
    <form id="id_form" action="어제문제정답.html" method="get" >
        아이디2 <input type="text" id="id_id1" name="nm_id1" value="" required><br>
        별명2 <input type="text" name="nm_alias2" value="" required><br>
        <input type="submit" value="전달2">
        <input type="reset" value="맨처음값으로2">
    </form>


    <script>
        var v_form = document.getElementById("id_form");
        /* 요즘은 거의 안 쓰는 방법 차라리 id로 접근하는 게 나음 
        var v_form1 = document.forms[0];
        var v_form2 = document.forms[1];
        console.log(v_form2);
        */

        v_form.onsubmit =function(){
            if(v_id.value.length <= 3){ // 세 글자 이하는 
                event.preventDefault(); // 전송 막기
            }
            return true;
        }


        var v_id = document.getElementById("id_id");
        function f_submit(){
            /* 원래 자바스크립트가 나왔던 이유, validation check라고 함 
            //if(!v_id.value) // 유효한 값을 안 쓰면 안 들어가게
            if(v_id.value.length < 3){// 세 글자 이상 써야만 넘어가게
                return false;
            }
            return true;
            */
        }
        //alert(location.href); // action 페이지가 실행됨을 확인 
    </script>
</body>
</html>
```

#### PHP test
```php
<?php
    //이 안에는 php만 해석할 수 있다.
    //문자열 더하기는 .으로 표시
    echo "<h1>".$_GET["nm_name"]."최고의 프로그래머</h1>";
    //echo phpinfo(); // php 설치정보를 보여주는 함수
    //"</body></html>";
?>
```

#### 인코딩
```html
<!DOCTYPE html>
<meta charset="UTF-8">
<script>
    /*      인코딩                    디코딩
    escape                   unescape               아주 옛날 거 
    encodeURI                decodeURI              조금 옛날 거(아직 조금은 사용됨)
    encodeURIComponent       decodeURIComponent     지금 사용하는 거 
    */
   var v_values = location.href;
   var v_queryString = v_values.split("?")[1];
   alert(docodeURIComponent(v_queryString));
   alert(encodeURIComponent(docodeURIComponent(v_queryString)));
   /*
    v_values = decodeURIComponent(v_values);
    v_values = decodeURIComponent(v_values); 
    alert(v_values);
    */

   
    </script>
```

## 📚 20일차

#### 비디오
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
                video::cue {
                font-size: 25px;
                color:red;
                background-color:yellow;
                opacity: 0.5;  /* 0은 완전 투명, 1은 완전 안투명  */
                line-height: 30px; /*텍스트를 담은 상자의 높이 */
            }
    
    </style>
</head>
<body>
    <video id="id_mv" width="400" src="./movie/movie1.mp4"
        controls muted controlslist="nodownload">
        <track src="sample-en.vtt" kind="subtitles" srclang="en" label="English"></track>
        <track src="sample-ko.vtt" kind="subtitles" srclang="ko" label="한국어" default></track>
    </video>
    <hr>

    <input type="button" value="플레이" onclick="f_play()">
    <input type="button" value="잠깐 멈춰" onclick="f_pause()">
    <input type="button" value="다음" onclick="f_next()">
    <input type="button" value="빠르게" onclick="f_fast()">

    <script>
        var v_mv=document.getElementById("id_mv");
        var v_index = 1;

        function f_fast(){
            v_mv.playbackRate = v_mv.playbackRate*2; //playbackRate: 속도
        }

        // 현재 플레이되는 동영상이 끝났다면 
        v_mv.onended = function(){ // onended: 영상 끝나고 뭐할지
            f_next(); // 다음 영상으로
            f_play(); // 강제 플레이
        }

        function f_play(){
            v_mv.muted = false; //위에 muted를 false로 만들어서 재생 누르면 소리 남
            v_mv.play(); //play: 재생
        }
        function f_pause(){
            v_mv.pause(); //pause: 멈춤
        }

        function f_next(){
            v_index++; 
            if(v_index >5) v_index = 1;
            v_mv.src = "./movie/movie"+ v_index+ ".mp4";
        }
    </script>
</body>
</html>
```

#### sample-ko.vtt
```vtt
WEBVTT FILE
 Note 여기 주석이예요!                
00:00:00.000 --> 00:00:02.000 line:10%
<b>안넝하세요~</b>
 00:00:02.000 --> 00:00:04.000  line:70% position:20%
<i>스크립트가 제일 쉬워요!~</i>
 00:00:05.000 --> 00:00:06.000 position:30%
<u>이렇게 쉬운 언어가 있어요</u>
```

#### sample-en.vtt
```vtt
WEBVTT FILE
 Note 여기 주석이예요!              
00:00:00.000 --> 00:00:02.000 line:10%
<b>Hello Hello~</b>
 00:00:02.000 --> 00:00:04.000  line:70% position:50%
<i>Script is really Easy!~</i>
 00:00:05.000 --> 00:00:06.000 position:30%  align:right
<u>Lier Lier Lier Lier</u>
```

#### 시계 만들기
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    #id_clock{
        width:200px;
        height:100px;
        background-color: black;
        color:yellow;
        font-size: 20px;
        line-height: 100px;
        text-align: center;
    }
</style>
</head>
<body>
    <div id="id_clock">
        <div id="id_inclock"></div>
    </div>
    <script>
        //날짜 객체(Date)
        //var v_date = new Date('서버시간세팅');//시스템의 현재 날짜 시간을 읽어옴 
        /*
        var v_date = new Date();
        alert("년도 " + v_date.getFullYear());
        alert("월 " + v_date.getMonth()); //주의 0부터 시작이라서 +1 해야됨
        alert("일 " + v_date.getDate());
        alert("요일 " + v_date.getDay()); // 일요일 0, 월요일1 ~ 토요일6
        alert("시간 " + v_date.getHours());
        alert("분 " + v_date.getMinutes());
        alert("초 " + v_date.getSeconds());
        alert(v_date.toLocaleString())//눈으로 보자
        */

        //디지털 시계 만들기

        var v_clock = document.getElementById("id_clock");
        function f_clock(){
            var v_date = new Date(''); 
            var v_hours = v_date.getHours();
            if(v_hours < 10){
                v_hours = "0" + v_hours;
            }
            var v_minutes = v_date.getMinutes();
            if(v_minutes < 10){
                v_minutes = "0" + v_minutes;
            }
            var v_seconds = v_date.getSeconds();
            if(v_seconds < 10){
                v_seconds = "0" + v_seconds;
            }

            var v_timeStr = v_hours + ":" + v_minutes + ":" + v_seconds; 

            v_clock.innerHTML = v_timeStr;
            setTimeout(f_clock,1000); //1초마다 재귀호출
        }


    </script>
</body>
</html>
```

#### 달력
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #id_cal{
            width: 720px;
            height: 630px;
            border: 1px solid black;
        }
        .cl_day{
            display: inline-block;
            font-size: 30px;
            text-align: center;
            width: 100px;
            height: 100px;
            line-height: 100px;
            border: 1px solid palevioletred;
            vertical-align: top; /* div 사용시 자주 만나는 정렬 문제 */

        }
    </style>
</head>
<body>

    <div id="id_cal"></div>
    <script>
        //날짜 다룰 때 가장 귀찮은 것.. 윤년, 달의 마지막 날이 며칠인가(실제는 2월)
        //1일에서 하루를 빼면 전월 마지막날이 나옴 
        //월의 마지막날 구하는 함수 
        var v_cal = document.getElementById("id_cal"); 
        //년도
        var v_year = document.createElement("select");
        for(var i=1; i<=6; i++){
            var v_yearOpt = document.createElement("option");
            v_yearOpt.value = "202"+i; 
            v_yearOpt.innerHTML = "202" +i; 
            v_year.appendChild(v_yearOpt); 
        }
        document.body.appendChild(v_year);

        //월
        var v_month = document.createElement("select");
        for(var i=1; i<=12; i++){
            var v_monthOpt = document.createElement("option");
            if(((new Date()).getMonth()+1)==i){
                v_monthOpt.selected = true; 
            }
            v_monthOpt.value = i; 
            v_monthOpt.innerHTML = i; 
            v_month.appendChild(v_monthOpt); 
        }
        document.body.appendChild(v_month);
        document.body.appendChild(v_cal);

        v_month.onchange = function(){
            selected
            alert("바꾸었습니다");
        }
        
        // var v_date = new Date("2021-03-01");
        // var v_last = v_date.setDate(v_date.getDate() - 1);
        // alert(v_date.toLocaleString()); 

        function f_getLastDate(p_year, p_month){
            var v_date = new Date(p_year, p_month, 1);
            v_date.setDate(v_date.getDate() -1); 
            return v_date.getDate(); // 마지막 일 리턴  
        }

        //월의 1일이 무슨 요일인지 리턴하는 함수 
        function f_getFirstDate(p_year,p_month){
            var v_date = new Date(p_year, p_month-1, 1);
            return v_date.getDay(); //getDay: 요일 
        }

        var v_startDay = f_getFirstDate(2021,5); //시작 요일 
        var v_lastDay = f_getLastDate(2021,5); 
        var v_dayS=1; // 시작일 
        var v_dayColor = ["red", "black", "black", "green", "black", "black", "blue"]
        for(var i=0; i<42; i++){
            var v_day = document.createElement("div");
            if(i>=v_startDay && v_dayS<=v_lastDay){
                v_day.innerHTML = v_dayS;
                v_dayS++;
            }else{
                v_day.style.backgroundColor="gray";
            }
            v_day.style.color=v_dayColor[i%7];
            
            v_day.setAttribute("class","cl_day");
            v_cal.appendChild(v_day);
            /*
            if(i%7==0){
                v_day.style.color="red"
            }
            if(i%7==6){
                v_day.style.color="blue"
            }
            */
        }
    </script>
</body>
</html>
```

## 📚 21일차

#### location -> receive
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <form action="receive.html" method="GET">
        아이디 <input type="text" name="nm_id" value=""><br>
        별명 <input type="text" name="nm_alias" value=""><br>
        보유스킬 <br>
        오라클 <input type="checkbox" name="nm_skills" value="oracle">
        HTML <input type="checkbox" name="nm_skills" value="html">
        CSS <input type="checkbox" name="nm_skills" value="css">
        JS <input type="checkbox" name="nm_skills" value="js">
        JSP <input type="checkbox" name="nm_skills" value="jsp"> <br>
        <input type="submit" value="전송">
    </form>
    
</body>
</html>
```

#### receive(location에서 보낸 값 받기)
```html
<!DOCTYPE html>
<meta charset="UTF-8">

<script src="./js/jsp.js"></script> 
<!-- 밑에 코드를 js파일로 빼고 불러서 실행  -->
<script>


// // 아이디와 별명의 값만 뽑아내려 함 
//     //쿼리스트림에서 원하는 값 찾기 일반화 
//     var request = {};   //빈 객체 생성

//     // 1개만 리턴
//     request.getParameter = function(p_schName){ //메소드 추가
//         var v_urlStr = location.href;
//         if(v_urlStr.indexOf("?") != -1){
//             var v_queryString = v_urlStr.split("?")[1];
//             var v_params = v_queryString.split("&"); 
//             for(var i=0; i<v_params.length; i++){
//                 var v_name = v_params[i].split("=")[0];
//                 var v_value = v_params[i].split("=")[1];
//                 if(v_name == p_schName){
//                     return decodeURIComponent(v_value).replaceAll("+"," ");
//                 }
//             }
//         }
//         return null; // 이런 건 정하는 것임, 아예 없어가 못 찾았을 때
//     }

//     // 그룹으로 넘어간 값 배열로 리턴
//     request.getParameterValues = function(p_schName){
//         var v_urlStr = location.href;
//         var v_rsltArr = [];
//         if(v_urlStr.indexOf("?") != -1){
//             var v_queryString = v_urlStr.split("?")[1];
//             var v_params = v_queryString.split("&"); 
//             for(var i=0; i<v_params.length; i++){
//                 var v_name = v_params[i].split("=")[0];
//                 var v_value = v_params[i].split("=")[1];
//                 if(v_name == p_schName){
//                     v_rsltArr.push(decodeURIComponent(v_value).replaceAll("+"," "));
//                 }
//             }
//         }
//         if(!v_rsltArr.length){
//             return null;
//         }
//         return v_rsltArr; // 이런 건 정하는 것임, 아예 없어가 못 찾았을 때
//     }

    var v_skills= request.getParameterValues("nm_skills");

    var out = {};
    out.print = function(p_msg){
        document.write(p_msg);
    }
    out.println = function(p_msg){
        document.write(p_msg+"<br>");
    }

    var v_id = request.getParameter("nm_id");
    var v_alias = request.getParameter("nm_alias");
    out.print("<h1>" + v_id + " 님 별명은 " + v_alias + " 너무너무 반가워요<h1>");
    out.print("<h1>당신의 보유능력은 " + v_skills + "이군용</h1>");




    //아래와 같은 사용은 너무 불편, 일반화 시켜야 함 
    /*
    var v_urlStr = location.href;
    var v_queryString = v_urlStr.split("?")[1];//? 오른쪽에 있는 값 가져오기 
    //alert(v_queryString); //확인
    var v_param1 = v_queryString.split("&")[0];//& 왼쪽에 있는 값 가져오기
    var v_id = decodeURIComponent(v_param1.split("=")[1]);//= 오른쪽 값 가져오기
    */

</script>
```

#### jsp.js
```js
// 아이디와 별명의 값만 뽑아내려 함

/*
서버 프로그램 없이 마치 서버 프로그램이 움직이는 것처럼 현재 사기를 치고 있음
그것이 가능한 이유는?
요청 내용이 주소 표시줄에 남아있는 것을 이용했기 때문
결국 get 방식으로만 가능하다. POST방식으로는 불가능
*/

//쿼리스트림에서 원하는 값 찾기 일반화
var request = {}; //빈 객체 생성

// 1개만 리턴
request.getParameter = function(p_schName){ //메소드 추가
var v_urlStr = location.href;
if(v_urlStr.indexOf("?") != -1){
var v_queryString = v_urlStr.split("?")[1];
var v_params = v_queryString.split("&");
for(var i=0; i<v_params.length; i++){
var v_name = v_params[i].split("=")[0];
var v_value = v_params[i].split("=")[1];
if(v_name == p_schName){
return decodeURIComponent(v_value).replaceAll("+"," ");
}
}
}
return null; // 이런 건 정하는 것임, 아예 없어가 못 찾았을 때
}

// 그룹으로 넘어간 값 배열로 리턴
request.getParameterValues = function(p_schName){
var v_urlStr = location.href;
var v_rsltArr = [];
if(v_urlStr.indexOf("?") != -1){
var v_queryString = v_urlStr.split("?")[1];
var v_params = v_queryString.split("&");
for(var i=0; i<v_params.length; i++){
var v_name = v_params[i].split("=")[0];
var v_value = v_params[i].split("=")[1];
if(v_name == p_schName){
v_rsltArr.push(decodeURIComponent(v_value).replaceAll("+"," "));
}
}
}
if(!v_rsltArr.length){
return null;
}
return v_rsltArr; // 이런 건 정하는 것임, 아예 없어가 못 찾았을 때
```
#### 로컬스토리지
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var v_str = " 1 + 2 * 6 - 3 + 6 / 2 * 21";
        alert(eval(v_str));
        eval("localStorage.aaa = 'kkkk'"); 
        /*
            eval 함수는 문자열에 대해서 javascript엔진을 구동시킴
            해킹에 많이 이용되어서 사용이 자제되고 있음. 일부 브라우져들은 eval함수가 소스에
            있으면 그 내용을 추적함
        */

// localStorage, 브라우져 내의 저장공간, 지우기 전에는 안 지워짐
        // 버퍼로 사용할 수 있음, 쿠키 대용으로 사용하면 아주 좋음, 현재 크롬은 5m 정도의 용량 지원
        // length
        // setItem, getItem, removeItem, key, clear

        // localStorage는 문자열 저장만 허락한다. 객체는 자동으로 타입을 표시하는 문자열이
        // 저장되어서, 그 내용을 잃어버리게 된다. 곧 내용을 잃어버리게 되어버림

    //write 기능
        var v_str = '{"name":"ssw"}'; //문자열 주의!! : 밖을 ''로 안을 ""로
        var v_obj = {"name":"ssw"};   //객체
        var v_arr = ["1","2","3","4"];

        //json <--> string 변환 유틸리티
        v_str = JSON.parse(v_str); //문자열을 JSON으로, 문자열이 JSON 문법에 맞아야만 함 
        alert(v_str.name); 

        v_obj - JSON.stringify(v_obj);//JSON을 문자열로  

        localStorage.setItem("hsg",JSON.stringify(v_obj)); 
        localStorage.setItem("ssw",JSON.stringify(v_arr));
    
    //꺼내 보기
        var v_check = JSON.parse(localStorage.getItem("ssw"));
        console.log(v_check[0]);

        var v_ssw = localStorage;
        //이렇게 사용도 가능 
        v_ssw.setItem("kkk", "hello"); //이걸 권장
        v_ssw.kkk2="hello2";

        localStorage.setItem("사승원","123");
        localStorage.setItem("사승원1","123");
        localStorage.setItem("사승원","456"); //주의! 같은 키 값이 들어가면 뒤에 있는 벨류 값으로 덮어써짐

    //읽기 기능
        //alert(localStorage.getItem("사승원1"));

    //지우기 기능
        //localStorage.removeItem("사승원1");
        //alert(localStorage.length); // 2
        //alert(localStorage.key(1)); // index번호로 넘겨주면 key값을 돌려줌 
        localStorage.clear(); //전부 지우기
    </script>

</body>
</html>
```
#### 테이블 만들기
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="id_disp"></div>
    <script>
        var v_commonTable = {
           grade01:"대표",
           grade02:"임원",
           grade03:"PM",
           grade04:"개발자"
        };
 
        var v_sawonList = [
           {level:"grade01",name:"로제"},
           {level:"grade04",name:"지민"},
           {level:"grade04",name:"정국"},
           {level:"grade03",name:"제이홉"},
           {level:"grade02",name:"제니"},
           {level:"grade04",name:"슈가"},
           {level:"grade02",name:"지수"},
        ];

        // table 만들때는 document.createElement를 잘 사용하지 않음
        // table만들때는 문자열 더하기가 훨씬 더 편하고 가독성도 좋음
        var v_tblStr = "<table border=2>";
        v_tblStr += "<tr><th>넘버</th><th>이름</th><th>직위</th></tr>"    
        for(var i=0; i<v_sawonList.length; i++){
            v_tblStr += "<tr>";
            v_tblStr += "<td>"+ (i+1) +"</td>";
            v_tblStr += "<td>"+ v_sawonList[i].name +"</td>";
            v_tblStr += "<td>"+ v_commonTable[v_sawonList[i].level] +"</td>"; // 사용에 주의
            v_tblStr += "</tr>";
        }
        v_tblStr += "</table>";
        document.getElementById("id_disp").innerHTML = v_tblStr;  // 화면 출력

    </script>
</body>
</html>
```


#### 오늘의 문제 - 수정필요
```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <select id="id_sel1" size=4 onchange="f_first()">
    </select>
    <select id="id_sel2" size=4 style="width:100px" onchange="f_second()">
    </select>
    <select id="id_sel3" size=4 style="width: 100px;">
    </select>
    <script>
        var v_grp1 = ["영업부","관리부"];
 
        var v_grp12 = [
            ["국내영업","해외영업","마구영업"],
            ["인사관리","구매관리","자금관리"]
        ];
 
        var v_grp123 = [
            [
                ["임나연","유정연","박지효"],
                ["김다현","손채영","박로제"],
                ["태리사","김제니","김지수"]
            ],
            [
                ["김남준","김석진"],
                ["민윤기","정호석","전정국"],
                ["박지민","김태형"]
            ]
        ];
 
 
        var v_str="<option>선택하세요</option>";
        for(var i=0; i < v_grp1.length; i++){
            v_str += "<option value="+ i + " >"+ v_grp1[i] + "</option>";
        }
        document.getElementById("id_sel1").innerHTML = v_str;
        //console.log(document.getElementById("id_sel1").innerHTML);
 
        // var v_selectStr = v_str.value
        // function f_select(){

        // }

        function f_first(){
           //코드 추가
           var v_selIndex = document.getElementById("id_sel1").value;
           var v_str1="<option>선택하세요</option>";
           for(var i=0; i < v_grp12.length+1; i++){
                for(var j=0; j < v_grp12.length+1; j++)
                v_str1 += "<option value="+ i + " >"+ v_grp12[i][j]+ "</option>";
                // if(v_selIndex == 0){
                //     v_grp12[][]
                // }
        }
        document.getElementById("id_sel2").innerHTML = v_str1;
        console.log(v_selIndex);
        }
 

        function f_second(){
           //코드 추가
           var v_selIndex2 = document.getElementById("id_sel12").value;
           var v_str2="<option>선택하세요</option>";
           for(var i=0; i < 2; i++){
                for(var j=0; j < 3; j++){
                    for(var k=0; k < 2; k++){
                        v_str2 += "<option value="+ i + " >"+ v_grp123[i][j][k]+ "</option>";

                    }
                }
 
        }
        document.getElementById("id_sel3").innerHTML = v_str2;
        }
        
    </script>    
</body>
</html>
```


#### 오늘의 문제 - 힌트
```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <select id="id_sel1" size=4 onchange="f_first()">
    </select>
    <select id="id_sel2" size=4 style="width:80px" onchange="f_second()">
    </select>
    <select id="id_sel3" size=4 style="width:80px">
    </select>
    <script>
        var v_grp1 = ["영업부", "관리부"];

        var v_grp12 = [
            ["국내영업", "해외영업", "마구영업"],
            ["인사관리", "구매관리", "자금관리"]
        ];

        var v_grp123 = [
            [
                ["임나연", "유정연", "박지효"],
                ["김다현", "손채영", "박로제"],
                ["태리사", "김제니", "김지수"]
            ],
            [
                ["김남준", "김석진"],
                ["민윤기", "정호석", "전정국"],
                ["박지민", "김태형"]
            ]
        ];

        var v_str = "<option>선택하세요</option>";
        for (var i = 0; i < v_grp1.length; i++) {
            v_str += "<option value=" + i + " >" + v_grp1[i] + "</option>";
        }
        document.getElementById("id_sel1").innerHTML = v_str;

        function f_first() {
            //힌트
            var v_selIndex = document.getElementById("id_sel1").value;
            var v_selBuseo = v_grp12[v_selIndex];
            
            var v_str = "<option>선택하세요</option>";
            for (var i = 0; i < v_selBuseo.length; i++) {
                v_str += "<option value=" + i + " >" + v_selBuseo[i] + "</option>";
            }
            document.getElementById("id_sel2").innerHTML = v_str;
        }

        function f_second() {
            //코드 추가
        }
    </script>
</body>

</html>
```


## 📚 22일차

#### 숫자누적(SUM)
```html
<!DOCTYPE html>
<meta charset="UTF-8">
<script>

    var v_sum = 0;  // 숫자 누적
    for(;"일단사용자가0입력할때까지 무한루핑";){
        var v_userIn = parseInt(prompt("숫자를 입력하세요,종료는 0입력","1"));
        if(v_userIn == 0){
            alert("지금까지의 합은 " + v_sum + " 입니다");
            break;        // 종료
        }
        v_sum += v_userIn;
    }
</script>
```

#### 사칙연산
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var v_num1 = parseInt(prompt("첫 번째 숫자를 입력해주세요", "1")); //default값 1로 지정
        var v_num2 = parseInt(prompt("두 번째 숫자를 입력해주세요", "1")); //default값 1로 지정
        var v_op = prompt("연산자를 입력해주세요" + "+");                 //default값 + 로 지정

        var v_result;
        if(v_op=="+"){
            v_result = v_num1 + v_num2;
        }else if(v_op=="-"){    
            v_result = v_num1 - v_num2;
        }else if(v_op=="*"){
            v_result = v_num1 * v_num2;
        }else if(v_op=="/"){
            v_result = v_num1 / v_num2;
        }else{
            alert("사칙 연산만 지원합니다")
            v_result = "사칙 연산만 지원합니다!"
        }

    </script>
    
</body>
</html>
```

#### for-in문
```html
<!DOCTYPE html>
<meta charset="UTF-8">
<script>
    /*
    var v_arr=["사승1", "사승2", "사승3"]; 
    for(var v_ssw in v_arr){
        alert(v_ssw + v_arr[v_ssw]);
    }       값 : 0 1 2 3         
    */  

   var v_json = {}; 
   v_json.att1 = "사승1";
   v_json.att2 = "사승2";
   v_json.att3 = "사승3";
   v_json.method1= function(){
       return;
   }

   //v_json.att1 은 v_json["att1"]과 같다
   for(var v_attr in v_json){
       alert(v_attr +  " " + v_json[v_attr]);
   } 

</script>
```

## 📚 23일차

#### select문제
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    #container {
        width:320px;
        border:1px solid black;
    }
    .cl_ktj {
        display: inline-block;
        width:100px;
       /* border:1px solid hotpink;*/
        vertical-align: top;
        text-align: center;
    }
</style>
</head>
<body>
<h1>select 문제3</h1>
<!--
    힌트: appendChild를 이용해서 이미 화면에 존재하는 객체를 다른 곳에 붙여 넣으면 이동하게 됨
-->
<div id="container">
    <div class="cl_ktj">
        <select id="id_sel1" size=8 multiple style="width:50px">
            <option value="1">1</option>
            <option value="3">3</option>
            <option value="5">5</option>
            <option value="7">7</option>
        </select>
    </div>
    <div class="cl_ktj">
        <br>
        <input id="id_lr" type=button value=">"><br>
        <input id="id_lrall" type=button value=">>"><br>
        <input type=button value="<"><br>
        <input type=button value="<<"><br>
    </div>
    <div class="cl_ktj">
        <select id="id_sel2" size=8 multiple style="width:50px">
            <option value="2">2</option>
            <option value="6">6</option>
            <option value="8">8</option>
        </select>
    </div>
</div> 
<input id="id_txt" type=text value=""><input id="id_btn" type=button value="추가하기">
<script>
    var v_txt = document.getElementById("id_txt");
    var v_btn = document.getElementById("id_btn");
    var v_sel1 = document.getElementById("id_sel1");
    var v_sel2 = document.getElementById("id_sel2");
    var v_lr = document.getElementById("id_lr");
    var v_lrall = document.getElementById("id_lrall");

    var v_sel1Options = v_sel1.options;
    v_lr.onclick=function(){
        for(var i=0; i< v_sel1Options.length; i++){
            if(v_sel1Options[i].selected){
                v_sel2.appendChild(v_sel1Options[i]);
                i--;  // 빈 공간을 뒤에 께 와서 채우기 때문에 i값 증가하지 못하게 해야 함
            }
        }
    }

    v_lrall.onclick=function(){
        for(;v_sel1Options.length != 0;){
            v_sel2.appendChild(v_sel1Options[0]);
        }
    }

    v_btn.onclick = function(){
        var v_option = document.createElement("option");
        v_option.innerHTML = v_txt.value;
        v_sel1.appendChild(v_option);  // select에 option 추가 
    }

</script>   
</body>
</html>
```

#### node 쓰지말자
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- 속성이나 메소드이름에 Node가 들어간 건 다루기가 애매한 부분이 있으니 사용을 자제한다. -->
    <div id="par">
        <div id="chi"></div></div>
    <script>
        var v_par = document.getElementById("par");
        //console.log(v_par.children[0]);

        console.log(v_par.children[0]); 
        /* console.log("=================="); 
        console.log(v_par.childNodes[1]);
        console.log("==================");
        console.log(v_par.childNodes[2]); 
         */ 
    </script>
</body>
</html>
```

#### screen
```html
<!DOCTYPE html>
<meta charset="UTF-8">
<script>
    /* 거의 쓸 일 없다. */
    alert(navigator.userAgent); //사용자가 어떤 브라우저를 사용하는지 파악할 때 사용 
                                //인터넷 진흥원 같은 곳에서 사용

    history.go(2);  //앞으로 가기 버튼 2번 누른 효과
    history.go(-1); // 뒤로 가기 버튼 1번 누른 효과
    
    alert(screen.colorDepths); // 컬러 해상도 24bit 칼라지원 모니터 사용하고 있음 
    alert(screen.availHeight); 
    alert(screen.availWidth);


</script>
```

#### 주민번호 체크
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
    #id_disp {
        width: 250px;
        border:1px solid hotpink;
    }
</style>
</head>
<body>
    <div id="id_disp"></div>
    <h1>주민번호 체크</h1>
    <input id="id_jumin1" type=text value="">-<input id="id_jumin2" type=text value=""><br>
    <input id="id_check" type=button value="체크"><br>
    <input id="id_gazza" type=button value="가짜주민번호생성"><br>
<script>
    var v_jumin1 = document.getElementById("id_jumin1");
    var v_jumin2 = document.getElementById("id_jumin2");
    var v_check = document.getElementById("id_check");
    var v_gazza = document.getElementById("id_gazza");
    var v_disp = document.getElementById("id_disp");

    v_gazza.onclick=function(){
        var v_year = Math.round(Math.random()*60)  + 30;
        var v_month = Math.ceil(Math.random()*12);
        if(v_month < 10){
            v_month = "0" + v_month;
        }
        var v_date = Math.ceil(Math.random()*28);
        if(v_date < 10){
            v_date = "0" + v_date;
        }
        var v_apjari = ""+v_year + v_month + v_date;

        var v_dijari = ""+Math.ceil(Math.random()*2);
        for(var i=1; i<=5; i++){
            v_dijari += Math.round(Math.random()*9);
        }

        var M = f_returnM(v_apjari, v_dijari);
         // 출력
         v_disp.innerHTML +=  v_apjari + "-" + v_dijari + M + "<br>";
        
    }
    function f_returnM(p_ap, p_di){
        // text박스에서 개별 숫자 뽑아내깅
        var A = p_ap[0];
        var B = p_ap[1];
        var C = p_ap[2];
        var D = p_ap[3];
        var E = p_ap[4];
        var F = p_ap[5];
        var G = p_di[0];
        var H = p_di[1];
        var I = p_di[2];
        var J = p_di[3];
        var K = p_di[4];
        var L = p_di[5];

        //알고리즘 대로 총합 구하깅
        var totalHap = (A*2) + (B*3) + (C*4) + (D*5) + (E*6) + (F*7);
        totalHap = totalHap + (G*8) + (H*9) + (I*2) + (J*3) + (K*4) + (L*5);  

        //11로 나눈 나머지를 구하래용
        var checkNum = (11 - (totalHap % 11) ) % 10 ;    
        return checkNum;
    }

    function f_check(){
        // text박스에서 개별 숫자 뽑아내깅
        var A = v_jumin1.value[0];
        var B = v_jumin1.value[1];
        var C = v_jumin1.value[2];
        var D = v_jumin1.value[3];
        var E = v_jumin1.value[4];
        var F = v_jumin1.value[5];
        var G = v_jumin2.value[0];
        var H = v_jumin2.value[1];
        var I = v_jumin2.value[2];
        var J = v_jumin2.value[3];
        var K = v_jumin2.value[4];
        var L = v_jumin2.value[5];
        var M = v_jumin2.value[6];

        //알고리즘 대로 총합 구하깅
        var totalHap = (A*2) + (B*3) + (C*4) + (D*5) + (E*6) + (F*7);
        totalHap = totalHap + (G*8) + (H*9) + (I*2) + (J*3) + (K*4) + (L*5);  

        //11로 나눈 나머지를 구하래용
        var checkNum = (11 - (totalHap % 11) ) % 10 ;
        
        if(checkNum == M){
            alert("너 한국사람이구나?");
        }else {
            alert("외국인?");
        }

    }
    v_check.addEventListener("click",f_check); // 클릭하면 f_check 함수를 불렁


    v_jumin1.onkeydown = function(){
        /*
        if(v_jumin1.value.length == 6 ){
            v_jumin2.focus();      // 커서 이동            
        }
        */
        if(event.key == "Enter"){
            v_jumin2.focus();      // 커서 이동
        }
    }
</script>
</body>
</html>
```

#### 배열과 JSON
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <select id="id_sel">
        <option value="p">1승원</option>
        <option value="o">2승원</option>
        <option value="l">3승원</option>
        <option value="s">4승원</option>
    </select>
    <script>
        var v_sel = document.getElementById("id_sel");
        console.log(v_sel);
        console.dir(v_sel);// 객체 표기법으로 표현, 속성과 메소드 리스트를 확인할 때 유용
/*         
        for(var i=0; i<v_sel.length; i++){
            console.log(v_sel[i]);
            console.log(v_sel.options[i]);  // 가독성이 이것이 더 좋음
            console.log("==============================");
        } 
*/
    


/*         //배열과 JSON은 당연히 헷갈릴 수 있음, JSON표현에 배열식 접근법이 있으므로
        //key(속성)값의 데이터 타입은 문자열임 
        var select = {};
        select[0] = "사승1";
        select[1] = "사승2";
        select[2] = "사승3";
        select[3] = "사승4";
        select.options = [];
        select.options.push(select["0"]);
        select.options.push(select["1"]);
        select.options.push(select["2"]);
        select.options.push(select["3"]); 
        select.length = select.options,length; 

    for(var i=0; i<select.length; i++){
        // 아래 두 개의 출력 결과는 동일하다.
        console.log(select[i]); 
        console.log(select.options[i]);
    }
        // 아래 두 개의 출력 결과는 동일하다.
        console.log(select);
        console.log(select.options[0]); 
*/


    </script>
</body>
</html>
```

#### 마우스이벤트
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<style>
    #id_ngm{
        width: 200px;
        height: 200px;
        border: 2px solid black;
    }
    #id_ktj{
        width: 100px;
        height: 100px;
        border: 2px dotted palevioletred;
        position: relative;
        left: 100px;
        top: 100px;
    }
</style>
<body> 
    <!-- enter : 들어오면 동작 / leave : 떠나면 동작 -->
    <div id="id_ngm" onmouseenter="f_enter()" onmouseleave="f_enter2()">  
        <div id="id_ktj" onmouseenter="f_enter2()"></div>
    </div>
    <script>
        function f_enter(){
            alert("사승원");
        }
        function f_enter2(){
            alert("사승이");
        }
    </script>
</body>
</html>
```

#### 차트 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.9.4/Chart.min.js"></script>
<!--
    CDN : Contents Delivrey Network
-->
</head>
<body>
    <input type=button value="차트에속으면 돈 잃는당" onclick="f_chg()">
    <div style="width:400px;height:400px;">
        <canvas id="myChart"></canvas>
    </div>
<script>
    /*  2시간 30분
      4/1일 나올사람 : 
        10시 ~  19시  (식비 지참) 
        남기문, 김소민, 장두언, 황미선, 김주헌, 사승원, 박태환, 오성현, 이윤행 (확정자)
    */
    function f_chg(){
        //alert(myChart.data.datasets[0].data[1]); //?19
        //myChart.data.datasets[0].data[1] = 99;
        //myChart.type = "line";  이거 안됨
        for(var i=1; i<=6; i++){
            myChart.data.datasets[0].data[i]=Math.round(Math.random()*50)+20;
            myChart.data.datasets[1].data[i]=Math.round(Math.random()*50)+20;
        }

        myChart.data.datasets[0].type="line";  // 이거 됨
  //      myChart.data.datasets[0].data = [11, 22, 33, 44, 55, 66];
        myChart.update();  // 잊지말장 다시 그려야 해용
        setTimeout(f_chg,300);
    }
var ctx = document.getElementById('myChart').getContext('2d');
var myChart = new Chart(ctx, {
    type: 'bar',
    data: {
        labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
        datasets: [{
            label: '# of Votes',
            data: [12, 19, 3, 5, 2, 3],
            backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
            ],
            borderWidth: 1
        }]
    },
    options: {
        scales: {
            yAxes: [{
                ticks: {
                    beginAtZero: true
                }
            }]
        }
    }
});

var v_dataset = {
            type:"line",
            label: '# Gimun Dungap',
            data: [99, 88, 77, 66, 55, 44],
            backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
            ],
            borderWidth: 1
        }
myChart.data.datasets.push(v_dataset);
myChart.update();
</script>
</body>
</html>
```
