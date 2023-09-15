# DH Kang GitHub

GitHub blog :  https://heeyapro.github.io/
---
### 시큐어코딩 - 소프트웨어 개발보안 <br><br>

#### 참고 자료 및 교재
□ 소프트웨어 보안 약점 진단가이드 (2021) <br>
□ 공개SW를 활용한 소프트웨어 개발보안 점검 가이드 <br>
□ 소프트웨어 개발보안 가이드 (2021.12.29) <br>
□ Python 시큐어코딩 가이드 (2022년 개정본) <br>

■ [Burp suite] 프록시 툴 사용으로 취약점 파악 및 모의 해킹<br>
> 파악된 취약점 우회 방법이나 해결 방법 논의<br>

예) 파일 다운로드 취약점<br>
> replace() 사용 ../ (x) .. , /, \, //, \\ (o)<br>

■ 에러처리 (개발보안 가이드) pmd <br>
>실습 페이지 : http://61.39.155.24:50002/ (test, ')<br>
>403 : 페이지는 있는데 접근이 거부된 에러 //의도적 접근 (오류 메시지 정보 유출)<br>
>200 : 페이지가 열린다는 에러<br>
>http://61.39.155.24:50002/demoshop/login/<br>

>// 에러 메시지로 스택 정보가 노출됨<br>
>e.printStackTrace();<br>
>// 오류발생시 화면에 출력된 시스템 정보로 다른 공격의 빌미를 제공한다.<br>
>System.err.print(e.getMessage());<br>

>// 에러 코드와 정보를 별도로 정의하고 최소 정보만 로깅<br>
>logger.error("ERROR-01: 파일 열기 에러");<br>

##### App.java
Java의 기본 패키지인 Logger를 사용하여 내부 시스템에 로깅되도록 코드수정<br>
먼저, Java의 기본 패키지인 Logger를 사용하기 이해 import<br>
+ import java.util.logging.Level; //수준<br>
+ import java.util.logging.Logger; //로깅<br>
그리고 생성자에서 Logger 객체를 생성<br>
+private static Logger logger = Logger.getLogger(App.class.getName()); //자세한 loging 에 대해 알려줌. (getName())<br>
INFO 수준의 에러가 발생한 자세한 메시지를 로깅되도록 수정<br>
-ioe.printStackTrace();<br>
+logger.log(Level.INFO, ioe.getMessage(), ioe);<br>

##### MainController.java 135-138 SystemPrintln
+ import java.util.logging.Level; //수준<br>
+ import java.util.logging.Logger; //로깅<br>
+	private static Logger logger = Logger.getLogger(MainController.class.getName());<br>
+ System.out.println( -> logger.log(Level.INFO, <br>

■ 에러처리 (개발보안 가이드) spot <br>

##### Tools.java (Spot Bugs)
SecureMailer -> Scary -> Normal confidence -> ... -> This API <br>
1. 경로조작 취약점 //도구가 알려준 솔루션 <br>
2. 취약한 예 <br>
File file = new File("resources/images/", image); //Weak point <br>
3. 안전한 코드<br>
File file = new File("resources/images/", FilenameUtils.getName(image)); //Fix <br>
4. 안전한 코드 수정<br>
+import org.apache.commons.io.FilenameUtils;// 자바 기본 패키기가 아님. 자료 파일을 추가해야함.<br>
=> https://commons.apache.org/proper/commons-io/download_io.cgi -> commons-io-2.13.0-bin.zip <br>
=> SecureMailer -> Properties for SecureMailer -> Java Build Path -> Add External JARs -> commons-io-2.13.0.jar -> apply and close <br>
=> ctrl + HTML_TEMPLATE_LOCATION 첫번째 클릭 <br>
- File file = new File(String.format("%s\\%s.txt", Constants.HTML_TEMPLATE_LOCATION, filename, ".txt"));<br>

+ String path = "C:\\SecureCoding_Expert\\workspace\\SecureMailer\\src\\resources\\template";<br>
+ path = path + "\\" + FilenameUtils.getName(filename) + ".txt";<br>
+ File file = new File(path); <br>

##### EmailEngine.java (Spot Bugs)
without null check // null 검증을 해야 쓰레기 값이 안 들어감.<br>
1. 검증 누락<br>
1) message.setSubject(subject);<br>
2) message는 EmailEngine 클래스의 멤버값이고, 초기화 되지 않았기 때문에 null 일 수 있음.<br>

2. 생성자에서 message 값을 초기화! <br>
33: +message = null; <br>

3. 취약한 라인에서 null 체크 소스코드 추가
62: + if(message != null) {} <br>
[수정]<<br>
if(message != null) {	<br>
				message.setSubject(subject); <br>
        	} <br>


### 인공지능 기반 운전자 식별 및 침입탐지시스템
□ 머신러닝 알고리즘 종류 파악 (현재 사용 알고리즘 Random Forest, Extra Trees, GSboots)<br>
□ 딥러닝 알고리즘 파악 (sota model 사용 예정)<br>
□ dataset : HCRL Driving dataset (추후 여러 데이터 사용 예정)<br>
