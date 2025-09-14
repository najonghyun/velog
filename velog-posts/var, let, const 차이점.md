<h3 id="크게-선언-및-재할당과-범위scope로-나뉜다">크게 선언 및 재할당과 범위(Scope)로 나뉜다.</h3>
<h4 id="선언-및-재할당">선언 및 재할당</h4>
<ul>
<li><strong>var</strong> : 중복선언 가능, 재할당 가능</li>
<li><strong>let</strong> : 중복선언 불가, 재할당 가능</li>
<li><strong>const</strong> : 중복선언 불가, 재할당 불가</li>
</ul>
<h4 id="범위-scope">범위 (Scope)</h4>
<ul>
<li><strong>var</strong> : 함수 레벨 스코프, 함수안에서만 범위가 지역한정이고 나머지 if, loop문에서는 외부 호출 가능</li>
<li><strong>let, const</strong> : 블록 레벨 스코프, 따라서 블록안에 있으면 외부에서 호출 불가</li>
</ul>
<blockquote>
<p><strong>호이스팅 (hoisting)</strong>
자바스크립트 파서가 실행 전에 함수 내에서 필요한 모든 변수를 마치 미리 <font color="red">선언</font>한 것처럼 내부적으로 끌어올려 처리해 동작하는 것</p>
</blockquote>
<ul>
<li><strong>var 호이스팅</strong> : 선언되기 전에 변수 참조시 에러가 아닌 undefined 발생</li>
<li><strong>let 호이스팅</strong> : 선언되기 전에 변수 참조시 에러 발생
<font color="red">이는 호이스팅은 되었지만 초기화가 이루어지지 않아 일시적 사각지대(TDZ)에 빠졌기 때문</font></li>
</ul>
<hr />
<h3 id="추가-개념">추가 개념</h3>
<blockquote>
<p><strong>렉시컬 스코프 (lexical scope)</strong>
        함수가 어디서 선언 하는지에 따라 상위 스코프를 결정하는 것을 의미 ↔ 동적 스코프 (어디서 호출하는지)</p>
</blockquote>
<blockquote>
<p><strong>TDZ (Temporal Dead Zone)</strong>
호이스팅은 되었지만, 아직 초기화 전이라 사용할 수 없는 구간, let과 const만 적용</p>
</blockquote>