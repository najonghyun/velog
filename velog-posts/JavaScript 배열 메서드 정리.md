<h3 id="배열을-순회하면서-조건에-맞는-요소를-찾거나-걸러내는-배열-내장-메서드를-하나씩-알아보자">배열을 순회하면서 조건에 맞는 요소를 찾거나 걸러내는 배열 내장 메서드를 하나씩 알아보자.</h3>
<h3 id="reduce">reduce()</h3>
<ul>
<li><p>*<em>목적 : *</em> 배열의 각 요소를 순회하며 callback함수의 실행 값을 누적하여 <em>하나의 결과값</em> 을 반환</p>
</li>
<li><p><strong>매개변수 :</strong> <code>callback</code></p>
<ul>
<li><font color="red"><code>accumulator</code></font> : 누적된 값</li>
<li><font color="red"><code>currentValue</code></font> : 현재 순회 중인 배열의 요소</li>
</ul>
<ul>
<li><code>initialValue</code> (선택적) : 첫 번째 호출에서 <font color="red"><code>accumulator</code></font>의 초기 값. 지정하지 않으면 배열의 첫 번째 요소가 초기값으로 사용됨</li>
</ul>
</li>
</ul>
<pre><code>const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// 예시 1 : initialValue 없는 경우
const sum1 = numbers.reduce((accumulator, currentNumber) =&gt; accumulator + currentNumber); // accumuulator 누적합 55 반환

// 예시 2 : initialValue 있는 경우
const sum2 = numbers.reduce((accumulator, currentNumber) =&gt; {
    return accumulator + currentNumber; // 0 + ... 으로 실행
}, 0);
</code></pre><hr />
<h3 id="map">map()</h3>
<ul>
<li><p>*<em>목적 : *</em> 배열의 각 요소에 대해 주어진 함수를 실행한 결과로 새로운 <em>배열</em> 을 반환하는 함수</p>
</li>
<li><p><strong>매개변수 :</strong> <code>callback</code></p>
<ul>
<li><font color="red"><code>currentValue</code></font> : 현재 순회 중인 배열의 요소</li>
<li><font color="red"><code>index</code></font> (선택적) : 현재 요소의 인덱스</li>
<li><font color="red"><code>array</code></font> (선택적) : 전체 배열</li>
</ul>
</li>
</ul>
<pre><code>const numbers = [1, 2, 3, 4, 5];

// 각 요소에 2를 곱한 새로운 배열 반환
const doubledNumbers = numbers.map((num) =&gt; num * 2);

console.log(doubledNumbers); // [2, 4, 6, 8, 10]</code></pre><hr />
<h3 id="filter">filter()</h3>
<ul>
<li><p>*<em>목적 : *</em> 배열에서 조건에 맞는 요소만을 필터링하여 새로운 <em>배열</em> 을 반환하는 함수</p>
</li>
<li><p>*<em>매개변수 : *</em><code>callback</code></p>
<ul>
<li><font color="red"><code>currentValue</code></font> : 현재 순회 중인 배열의 요소</li>
<li><font color="red"><code>index</code></font> (선택적) : 현재 요소의 인덱스</li>
<li><font color="red"><code>array</code></font> (선택적) : 전체 배열</li>
</ul>
</li>
</ul>
<pre><code>const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// 짝수만 필터링하여 새로운 배열 반환
const evenNumbers = numbers.filter((num) =&gt; num % 2 === 0);

console.log(evenNumbers); // [2, 4, 6, 8, 10]</code></pre><hr />
<h3 id="foreach">forEach()</h3>
<ul>
<li><p>*<em>목적 : *</em> 배열의 각 요소에 대해 주어진 함수를 실행하지만, <em>값을 반환하지 않고</em> 단순히 반복 작업을 할 때 사용</p>
</li>
<li><p>*<em>매개변수 : *</em><code>callback</code></p>
<ul>
<li><font color="red"><code>currentValue</code></font> : 현재 순회 중인 배열의 요소</li>
<li><font color="red"><code>index</code></font> (선택적) : 현재 요소의 인덱스</li>
<li><font color="red"><code>array</code></font> (선택적) : 전체 배열</li>
</ul>
</li>
</ul>
<pre><code>const numbers = [1, 2, 3, 4, 5];

// 배열의 각 요소를 콘솔에 출력
numbers.forEach((num) =&gt; {
  console.log(num);
});</code></pre><blockquote>
<p>** 반환값은 없고 단순히 작업만 반복! **</p>
</blockquote>
<hr />
<h3 id="some">some()</h3>
<ul>
<li><p>*<em>목적 : *</em>배열의 요소 중 하나라도 조건에 맞는 것이 있으면 <code>true</code>를 반환하는 함수입니다.</p>
</li>
<li><p>*<em>매개변수 : *</em><code>callback</code></p>
<ul>
<li><font color="red"><code>currentValue</code></font> : 현재 순회 중인 배열의 요소</li>
<li><font color="red"><code>index</code></font> (선택적) : 현재 요소의 인덱스</li>
<li><font color="red"><code>array</code></font> (선택적) : 전체 배열</li>
</ul>
</li>
</ul>
<pre><code>const numbers = [1, 3, 5, 7, 9];

// 배열에 짝수가 하나라도 있는지 확인
const hasEven = numbers.some((num) =&gt; num % 2 === 0);

console.log(hasEven); // false</code></pre><hr />
<h3 id="추가-개념">추가 개념</h3>
<ul>
<li>인코딩 및 디코딩<blockquote>
</blockquote>
</li>
<li><em>encodeURIComponent(val)*</em> // 인코딩</li>
<li><em>decodeURIComponent(val)*</em> // 디코딩</li>
</ul>
<ul>
<li>JSON 및 String 변환<blockquote>
</blockquote>
</li>
<li><em>JSON.stringify(val)*</em> // JSON to String</li>
<li><em>JSON.parse(val)*</em> // String to JSON</li>
</ul>