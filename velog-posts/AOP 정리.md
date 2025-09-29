<h3 id="aop-aspect-oriented-programming-관점-지향-프로그래밍">AOP (Aspect-Oriented Programming, 관점 지향 프로그래밍)</h3>
<ul>
<li><strong>정의</strong> : 핵심 비즈니스 로직과는 별개지만 여러 모듈에서 공통적으로 필요한 기능(=횡단 관심사, Cross-Cutting Concern)을 한 곳에 모아 처리하는 프로그래밍 기법</li>
</ul>
<p>🔹<strong>쉽게 말하면 ?</strong> : 반복되는 공통 로직(로깅, 권한체크 등)을 각 클래스마다 넣는 대신, 필요한 지점에만 주입할 수 있도록 만든 프로그래밍 패러다임이다.</p>
<hr />
<h3 id="spring-aop">Spring AOP</h3>
<ul>
<li>Spring은 프록시 기반의 AOP를 제공한다.</li>
</ul>
<blockquote>
<p>💡<strong>프록시</strong> : 원본 객체를 감싸서 대신 요청을 받고, 필요한 부가 기능을 수행한 뒤 실제 객체에 위임하는 대리 객체
ex) “대리인”이 먼저 전화를 받고 필터링한 뒤, 중요한 내용만 본인에게 전달하는 것과 같은 개념</p>
</blockquote>
<h4 id="프록시-객체-생성-방식">프록시 객체 생성 방식</h4>
<ul>
<li><p><strong>JDK 동적 프록시</strong></p>
<ul>
<li><p>자바 기본에서 제공하는 프록시 방식</p>
</li>
<li><p>인터페이스가 있는 클래스만 가능</p>
</li>
</ul>
</li>
<li><p><strong>CGLIB 프록시 (Code Generation Library)</strong></p>
<ul>
<li><p>바이트코드 조작 라이브러리로 클래스를 상속받아 프록시 생성</p>
</li>
<li><p>인터페이스 없어도 프록시 생성 가능</p>
</li>
</ul>
</li>
</ul>
<hr />
<h3 id="📚-aop-주요-용어">📚 AOP 주요 용어</h3>
<ul>
<li><p><strong>Aspect</strong> : 횡단 관심사를 모듈화한 단위
<code>ex) “로깅 기능”, “트랜잭션 관리 기능” 자체를 의미</code></p>
</li>
<li><p><strong>Join Point</strong> : 애플리케이션 실행 흐름에서 AOP를 적용할 수 있는 모든 지점
<code>ex) Spring AOP에선 &quot;메소드 실행 지점&quot;만 Join Point로 봄</code></p>
</li>
<li><p><strong>Pointcut</strong> : Join Point 중 실제로 AOP를 적용할 지점을 지정하는 표현식
<code>ex) execution(* com.example.service.*.*(..)) → 특정 패키지 모든 메소드</code></p>
</li>
<li><p><strong>Advice</strong> : 실제로 삽입되는 코드(=공통 기능)</p>
<blockquote>
<p><strong>시점에 따라 구분</strong>
<code>@Before</code> : 메소드 실행 전
<code>@After</code> : 메소드 실행 후 (성공/실패 무관)
<code>@AfterReturning</code> : 정상 리턴 후
<code>@AfterThrowing</code> : 예외 발생 시
<code>@Around</code> : 메소드 실행 전후 모두 제어</p>
</blockquote>
</li>
<li><p><strong>Weaving (위빙)</strong> : Pointcut + Advice를 실제 코드에 적용해서 실행 흐름에 끼워 넣는 과정</p>
</li>
</ul>
<hr />
<h3 id="주요-활용-사례">주요 활용 사례</h3>
<ul>
<li>로깅 (메소드 실행 시간, 파라미터, 결과 기록)</li>
<li>트랜잭션 처리</li>
<li>성능 모니터링 (메소드 실행 시간 측정)</li>
<li>보안/권한 체크 (메소드 접근 권한 확인)</li>
<li>중복 요청 체크, 공통 예외 처리 등</li>
</ul>
<hr />
<h3 id="동작-방식-spring-aop">동작 방식 (Spring AOP)</h3>
<ol>
<li><code>@Aspect</code> 클래스를 만들고, 그 안에 Advice 메소드를 정의</li>
<li>Advice 메소드에 <code>@Around</code>, <code>@Before</code>, <code>@After</code> 같은 어노테이션을 붙이고 포인트컷 표현식으로 <strong>“어떤 메소드에 적용할지”</strong>를 지정<pre><code class="language-java">@Aspect
@Component
public class LogAspect {
 @Around(&quot;@annotation(com.example.LogExecutionTime)&quot;) // 포인트컷 지정
 public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
      long start = System.currentTimeMillis();
     Object result = joinPoint.proceed(); // 원래 메소드 실행
     long end = System.currentTimeMillis();
     System.out.println(joinPoint.getSignature() + &quot; 실행 시간: &quot; + (end - start) + &quot;ms&quot;);
     return result;
 }
}</code></pre>
</li>
<li>애플리케이션 실행 시, Spring이 해당 Bean을 감싸는 프록시 객체를 생성</li>
<li>지정된 포인트컷 조건에 맞는 메소드가 호출되면, 실제 대상 객체를 직접 호출하는 대신 프록시 객체가 먼저 호출을 가로챔<pre><code class="language-java">@Service
public class MemberService {
 @LogExecutionTime // 여기서 가로챔
 public void joinMember() throws InterruptedException {
     Thread.sleep(500);
     System.out.println(&quot;회원 가입 처리 완료&quot;);
 }
}</code></pre>
</li>
<li>프록시 객체가 Advice를 실행하고, 필요한 경우 <code>joinPoint.proceed()</code>를 통해 원래의 비즈니스 메소드를 호출</li>
</ol>
<blockquote>
<p>💡 <strong>하나의 포인트컷으로 묶어서 지정 가능</strong></p>
</blockquote>
<pre><code class="language-java">@Pointcut(&quot;@annotation(org.springframework.web.bind.annotation.PostMapping) || &quot; +
            &quot;@annotation(org.springframework.web.bind.annotation.PutMapping) || &quot; +
            &quot;@annotation(org.springframework.web.bind.annotation.DeleteMapping) || &quot; +
            &quot;@annotation(org.springframework.web.bind.annotation.PatchMapping)&quot;)
public void allRequestMappings() {
}</code></pre>
<pre><code class="language-java">/// 한번에 지정가능
@Around(&quot;allRequestMappings()&quot;)
public Object aroundHttpMethods(ProceedingJoinPoint joinPoint) throws Throwable {
    // 공통 로직
    return joinPoint.proceed();
}</code></pre>
<hr />
<h3 id="추가-개념">추가 개념</h3>
<h4 id="프론트엔드-미들웨어와-비교">프론트엔드 미들웨어와 비교</h4>
<ul>
<li><p><strong>Middleware(미들웨어)</strong></p>
<ul>
<li><p>“요청 흐름”을 가로채고 가공하는 역할 <code>ex) Redux 미들웨어, Express 미들웨어</code></p>
</li>
<li><p>요청 → 미들웨어 체인 → 최종 처리기로 흐름 전달.</p>
</li>
</ul>
</li>
<li><p><strong>Spring AOP</strong></p>
<ul>
<li><p>“메소드 실행 흐름”을 가로채는 역할</p>
</li>
<li><p>특정 메소드 실행 전/후/예외 시점에 공통 기능을 삽입</p>
</li>
</ul>
</li>
</ul>
<blockquote>
<p>👉 <strong>공통점</strong> : 핵심 로직 외의 기능을 따로 분리
 👉 <strong>차이점</strong> : 미들웨어는 요청 흐름, AOP는 메소드 실행 흐름</p>
</blockquote>