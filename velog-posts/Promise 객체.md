<h3 id="javascript-비동기-처리에-사용되는-객체">javascript 비동기 처리에 사용되는 객체</h3>
<ul>
<li>자바스크립트에서 데이터를 처리할 때 <strong>비동기</strong>라는 개념을 자주 사용</li>
</ul>
<blockquote>
<p><strong>비동기(asynchronous) : 어떤 작업이 끝날 때까지 기다리지 않고 다음 코드를 실행할 수 있도록 하는 방식</strong></p>
</blockquote>
<h3 id="데이터-통신-시-비동기를-왜-사용해야-할까">데이터 통신 시 비동기를 왜 사용해야 할까?</h3>
<ul>
<li>서버에서 데이터를 가져올 때 응답이 올 때까지 프로그램이 멈춘다면 다른 기능을 사용할 수 없음</li>
</ul>
<p>👉 데이터를 받는 동안에도 나머지 코드가 계속 실행되도록 해야하기 때문에 비동기를 사용해야 한다!</p>
<h3 id="콜백-함수">콜백 함수</h3>
<ul>
<li><p>비동기에서 중요한 건 &quot;데이터를 언제 받았는가&quot;라는 시점인데, 이 시점을 처리하기 위해 <strong>콜백(callback) 함수</strong>를 사용</p>
</li>
<li><p><strong>하지만</strong> 콜백을 계속 중첩해서 사용하다 보면 코드가 지저분해지고, 가독성이 떨어진다. 이 현상을 <strong>콜백 지옥(callback hell)</strong>이라고 부른다.</p>
</li>
</ul>
<h3 id="이-문제를-해결하기-위해-나온-것이-promise-객체">이 문제를 해결하기 위해 나온 것이 Promise 객체</h3>
<ul>
<li><p>Promise는 비동기 작업이 끝났는지, 아직 진행 중인지, 실패했는지를 표현할 수 있음</p>
</li>
<li><p>이를 통해 비동기 코드를 더 직관적이고 깔끔하게 작성할 수 있고, <code>.then()</code> <code>.catch()</code> 체인이나 <code>async/await</code> 구문을 이용해 마치 동기 코드처럼 읽기 쉽게 다룰 수 있다.</p>
</li>
</ul>
<hr />
<h3 id="promise-생성">Promise 생성</h3>
<pre><code>const getData = () =&gt; {
    // 프로미스 객체
    return new Promise((resolve, reject) =&gt; {
        const data = fetch(url); // 비동기 작업 수행
        if(data)
            resolve(data);
        else
            reject(&quot;error&quot;);
    })
}</code></pre><ul>
<li><strong>매개변수 :</strong> <code>callback</code><ul>
<li><span style="color: red;"><code>resolve</code></span> : 성공 시 메서드</li>
<li><span style="color: red;"><code>reject</code> </span> : 실패 시 메서드</li>
</ul>
</li>
</ul>
<h3 id="➡️-이렇게-생성한-promise객체는-then과-catch-메서드-체이닝으로-후속-처리를-할-수-있음">➡️ 이렇게 생성한 Promise객체는 .then()과 .catch() 메서드 체이닝으로 후속 처리를 할 수 있음</h3>
<pre><code>// 프로미스 객체 반환
getData()
    .then((response) =&gt;{
        // 성공시 콜백 함수, 저장된 데이터 response로 받아올 수 있음!
    })
    .catch((error)=&gt;{
        // 실패시 콜백 함수
    })</code></pre><hr />
<h3 id="추가-개념">추가 개념</h3>
<h4 id="프로미스-3가지-상태-states">프로미스 3가지 상태 (States)</h4>
<ul>
<li><p><strong>Pending(대기)</strong> : 처리가 완료되지 않은 상태 👉 프로미스 객체만 생성한 상태 <code>new Promise()</code></p>
</li>
<li><p><strong>Fulfilled(이행)</strong> : 성공적으로 처리가 완료된 상태 👉 프로미스 실행 후 <code>resolve()</code> 호출</p>
</li>
<li><p><strong>Rejected(거부)</strong> : 처리 실패된 상태 👉 프로미스 실행 후 <code>reject()</code> 호출</p>
</li>
</ul>