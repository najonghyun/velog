<h3 id="크게-3가지로-구분한다">크게 3가지로 구분한다</h3>
<h3 id="1-컴포넌트별-상태관리-usestate">1) 컴포넌트별 상태관리 useState</h3>
<ul>
<li><strong>정의</strong> : 단일 컴포넌트(또는 좁은 트리) 내부의 UI 상태를 로컬로 관리함</li>
</ul>
<h4 id="장점">장점</h4>
<ul>
<li><p>가장 단순하고 러닝커브 낮음, <strong>보일러 플레이트</strong> 적음</p>
</li>
<li><p>리액트 내장이라 의존성 없음, 성능 예측 쉬움</p>
</li>
</ul>
<blockquote>
<p><strong>보일러 플레이트 : 여러 가지 상황에서 거의 또는 전혀 변경하지 않고 재사용할 수 있는 컴퓨터 언어 텍스트</strong></p>
</blockquote>
<h4 id="단점">단점</h4>
<ul>
<li><p>상태를 여러 컴포넌트에서 공유하기 복잡함 (컨텍스트 남발)</p>
</li>
<li><p>서버 데이터 캐싱/동기화 같은 <strong>비즈니스 상태</strong>엔 부적합</p>
</li>
</ul>
<hr />
<h3 id="2-웹클라이언트-전역-상태관리--redux--zustand">2) 웹(클라이언트) 전역 상태관리 – Redux / Zustand</h3>
<ul>
<li><strong>정의</strong> : 여러 컴포넌트에서 공유되는 클라이언트 상태(UI 전역값, 세션, 필터, 위젯 열림 상태 등)를 중앙에서 관리</li>
</ul>
<h3 id="redux">Redux</h3>
<h4 id="장점-1">장점</h4>
<ul>
<li><p>예측 가능한 단방향 데이터 흐름, 강한 개발자 도구(타임트래블, 디버깅)</p>
</li>
<li><p>미들웨어(Redux-Thunk/Saga 등)로 사이드이펙트 제어 가능</p>
</li>
</ul>
<h4 id="단점-1">단점</h4>
<ul>
<li>학습/보일러플레이트(예전엔 특히) → RTK(Redux Toolkit)로 많이 완화</li>
</ul>
<h3 id="zustand">Zustand</h3>
<h4 id="장점-2">장점</h4>
<ul>
<li><p>매우 가벼움(보일러플레이트 최소), 훅 기반 API, 학습 쉬움</p>
</li>
<li><p>셀렉터/부분 구독으로 렌더링 최소화 용이</p>
</li>
</ul>
<h4 id="단점-2">단점</h4>
<ul>
<li>팀 규모 커지고 미들웨어/아키텍처가 복잡해지면 패턴 합의가 필요</li>
</ul>
<hr />
<h3 id="3-서버에서의-상태관리-react-query">3) 서버에서의 상태관리 react-query</h3>
<ul>
<li><strong>정의</strong> : 서버에서 가져온 데이터를 가져오기/캐싱/동기화/리밸리데이션하는 라이브러리</li>
</ul>
<h4 id="장점-3">장점</h4>
<ul>
<li><p>캐싱, 재검증, 백그라운드 리패치, 에러/로딩 관리, pagination/infinite query 지원</p>
</li>
<li><p>낙관적 업데이트, <strong><code>mutation</code></strong> 후 자동 무효화 등 “서버 상태 라이프사이클” 내장</p>
</li>
<li><p>보일러플레이트 급감 → 데이터 패칭 코드의 생산성/안정성↑</p>
</li>
</ul>
<h4 id="단점-3">단점</h4>
<ul>
<li><p>전역 클라이언트 상태(버튼 토글, 모달 등)에는 과하다고 느낄 수 있음</p>
</li>
<li><p>캐시 전략/무효화 키 설계가 필요</p>
</li>
</ul>