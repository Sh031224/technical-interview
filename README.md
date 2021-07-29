# technical-interview

프론트엔드 면접 준비자료입니다. 수정사항은 `Pull Requests`로 알려주시면 감사하겠습니다.

1. doctype
    - html 문서의 버전에 대한 정보와 함께 문서를 어떻게 렌더링 하면 되는지 알리기 위한 지침.
    - 브라우저에 상관없이 일관된 레이아웃을 제공할 수 있게 해준다.
2. data- 속성
    - 추가적인 데이터를 DOM에 저장 할 수 있음.
3. svg vs canvas
    - svg: 벡터 그래픽을 생성하도록 설계된 XML 파일 형식 / 해상도 안깨지고 크기 늘리거나 줄일 수 있음
    - canvas: 자바스크립트를 이용하여 픽셀 단위로 이미지를 만듦
4. 표준모드 vs 비표준 모드
    - 브라우저는 옛버전과의 호환성을 위해 비표준 모드에서 과거의 브라우저처럼 페이지를 렌더링 할 수 있음.
5. 이벤트 버블링, 이벤트 캡쳐
    - 버블링은 상위 요소로 이벤트 전달 ( onClick 메서드로 구현, e.stopPropagation로 전파 중단 )
    - 캡쳐링은 상위에서 하위로 이벤트 전달 ( addEventListener의 3번째 인자로 capture 플래그를 둠 )
6. call-by-value call-by-reference
    - call by value: 함수 안에서 인자의 값이 변경되어도, 외부의 변수의 값은 변경 X. 값을 복사하기 때문에 메모리 사용량이 늘어남
    - call by reference: 함수 안에서 인자의 값이 변경되면, 외부의 변수 값도 함께 변경. 원래의 값에 영향을 주는 리스크 존재.
7. 자바스크립트 런타임
    - 자바스크립트가 돌아가는 실행환경을 자바스크립트 런타임이라고 부름.
    - 런타임은 자바스크립트 엔진(메모리 힙, 콜 스택), Web Apis, 이벤트 루프, 콜백 큐로 이루어짐.
    - 코드가 실행되면 Call Stack에 쌓이고, Stack에서는 선입후출 룰 대로 실행된다.
        - 비동기 함수가 실행된다면, Web API가 호출된다.
        - Web API는 비동기함수의 콜백함수를 Callback Queue에 밀어넣는다.
        - Promise는 Microtask Queue로, Timeout은 Task Queue로, RequestAnimationFrame은 Animation Frame으로 콜백함수를 밀어넣는다.
            - Event Loop는 Call Stack이 빈 상태가 되면 콜백을 Call Stack으로 이동시킨다. (동시성 지원)
        - 콜백 이동 우선순위는 Microtask Queue > Animation Frames > Task Queue 이다.
8. setTimeout 0ms
    - setTimeout 0ms를 실행하면 0초를 기다리고 즉시 실행되는 것이 아니다.
        - setTimeout 함수를 실행하게 되면 Web Apis를 호출하고, 그 동안은 계속 Call Stack에 여러 함수들이 들어가고 나오면서 함수들이 실행된다.
        - Web Apis에서 0초를 기다리고 Callback Queue로 넣는데, Event Loop는 Call Stack이 비어 있어야 Callback Queue에서 Call Stack으로 이동한다.
            - 만약 setTimeout 0ms 이후 3초가 걸리는 함수를 실행한다면, setTimeout의 콜백 함수는 3초 후에 실행되는 꼴이다.
            - setTimeout의 delay인자가 delay ms 후에 실행 되는 것을 보장하지 않는다는 사실을 알 수 있다. 정확히는 delay ms 후에 Callback Queue에 들어가는 것을 보장한다.
        - 사실 0초를 기다리진 않는다.
            - 최소값은 브라우저에 의해 결정되며 0ms가 아니다. 원래 브라우저는이 최소값을 10ms로 설정하지만 HTML5 사양 및 최신 브라우저에서는 4ms로 설정되어 있다.
9. 깊은복사 얕은복사
    - 원시값: boolean, string, number, undefined , null , symbol -> 깊은복사
    - 참조값: Object -> 얕은복사 (같은 메모리 공유)
10. Prototype
    - 자바스크립트는 프로토타입을 기반으로 상속을 구현하여 불필요한 중복을 제거함.
    - 객체의 프로토타입을 구현 해놓으면, 자식 객체와 프로토타입의 자산을 공유하여 사용 할 수 있음.
11. Symbol
    - 프로그램이 이름 충돌의 위험 없이 속성의 키로 쓰기 위해 생성하고 사용 할 수 있는 값
12. 스프레드 연산자
    - 배열, 객체를 복사 하거나 합칠 때 간단하게 사용할 수 있게 해주는 es6 문법
13. Promise
    - 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값을 나타내는 객체
14. HTML vs HTML5
    - 기존의 html 문서타입 보다 간결해짐.
    - 시멘틱 태그 추가.
    - 비디오와 오디오를 자체적으로 지원
15. 브라우저 동작과정
    - 특정 주소로 들어가면 서버에 요청이 전송.
    - 렌더링 엔진이 해당 페이지에 있는 html과 css를 해석하여 DOM 트리를 구축
    - DOM 트리와 css 정보를 담은 스타일 구조체를 연결시켜 렌더 트리를 만듦
    - 화면에 배치
    - Script 태그를 만나게 되면 javascript 코드를 위해 파싱을 중단
    - 제어 권한을 자바스크립트 엔진에게 넘기고, 자바스크립트 코드 또는 파일을 로드해서 파싱하고 
16. TypeScript 쓰는 이유
    - 컴파일 단계에서 타입 오류를 발견 할 수 있음.
    - ES6 지원
    - IDE와 같은 도구에게 타입 정보를 제공함으로써 더 큰 지원을 받을 수 있다.
17. yarn.lock & package.json
    - 의존성 트리에 대한 정보
18. 검색엔진 최적화
    - Title 태그와 meta 태그를 이용하여 사이트의 제목과 설명 등을 설정
    - 모바일 친화적으로 사이트를 개발
    - 시맨틱 태그 사용
    - 제목과 부제 등 h1~h6태그, p태그 등을 활용
19. CSR vs SSR
    - CSR: 초기 로딩 이후 페이지 전환이 빠르고 서버에 부담이 덜감. 검색 엔진 최적화 불리.
    - SSR: 검색 엔진 최적화. 페이지 이동시 지속적으로 서버에 요청하기 때문에 페이지 전환 느림.
20. article과 section 태그의 차이
    - article: 같은 성격/유형의 컨텐츠끼리 묶을 때 사용. 태그 안의 컨텐츠만으로 독립이 가능하면 article 사용 애플워치 os 에서 읽기모드로 접속 시 article을 기준으로 읽음
    - section: 같은 성격/유형의 컨텐츠끼리 묶을 때 사용.
21. padding과 margin의 차이
    - margin: 바깥쪽 여백
    - padding: 안쪽 여백
22. inline vs block
    - inline: width/height 적용 불가 / margin/padding bottom top 적용 불가
    - block: 무조건 줄바꿈 적용 width/height 등 적용 가능
23. css selector 우선순위
    - !important > inline style > #id > .class/속성/가상 선택자 > 태그 > * 전체
24. es6 문법 중 생각나는대로 말해달라
    - 화살표 함수 (람다식)
    - let, const
    - class
    - export, import 를 이용하여 다른 곳에서도 함수나 변수를 활용 가능
    - spread 연산자
25. var, let, const 차이점
    - var은 함수 레벨 스코프를 지원, let,const는 블록레벨 스코프를 지원한다.
    - var 사용시 블록 레벨에 전역 변수를 다시 재선언 하는 경우 해당 변수를 다시 선언한 값으로 읽음.
26. use strict
    - 기존에는 무시하던 에러들을 throwing함.
    - JavaScript 엔진의 최적화 작업을 어렵게 만드는 실수들을 바로잡음.
27. callback을 왜 사용하는지?
    - 하나의 작업을 시켜두고 작업이 완료 되었을 때 해당 함수를 실행하여 순차적으로 진행이 가능
28. callback vs promise vs async await 차이
    - callback은 중첩해서 많이 사용하면 가독성이 매우 떨어짐
    - promise는 then을 통해 프로미스 체이닝이 되어 있어서 실행 순서를 쉽게 파악 가능하고, 가독성도 깔끔. 또 catch로 각 작업의 에러를 핸들링 가능
    - Async/await은 promise를 좀 더 간략하고 직관적으로 알아 볼 수 있도록 promise를 지원
29. react를 사용하는 이유?
    - SPA: Client Side Rendering으로 빈 html 파일에서 스크립트로 안의 요소들을 채워나감으로 화면간 전환이 매우 빠름
    - 화면의 한 부분을 컴포넌트라는 단위로 나누어 독립적으로 관리 할 수 있음.
    - 가상의 DOM을 두어, 이전의 DOM과 비교하여 실제 변경된 부분만 DOM에 적용시켜 성능 개선
    - 대규모 커뮤니티가 이미 형성되어 있어 자료를 찾기 매우 편리
30. 클래스 객체 인스턴스
    - 클래스(Class): 객체를 만들어내기 위한 설계도 혹은 틀
    - 객체(Object): 설계도(클래스)를 기반으로 선언된 대상, 클래스의 인스턴스 라고도 부름
    - 인스턴스(Instance): 객체에 메모리가 할당되어 실제로 활용되는 실체
31. 라이브러리 vs 프레임워크
    - 라이브러리: 사용자가 전체적인 흐름을 만들며 라이브러리를 가져다 씀
    - 프레임워크: 프레임워크가 전체적인 흐름을 쥐고 있으며 사용자는 그 안에서 필요한 코드를 짜 넣음
32. TCP vs UDP
    - TCP: 연결형 서비스, UDP보다 전송속도 느림, 신뢰성 있는 데이터를 전송함.
    -  연속성보다 신뢰성있는 전송이 중요할 때에 사용
    - UDP: 비연결형 서비스, TCP와 다르게 정보를 주고 받을 때 정보를 보내거나 받는다는 신호 절차를 거치지 않음.
    - 신뢰성 보다는 연속성이 중요한 실시간 서비스에 자주 사용
33. 클로저
    -  자신이 선언되었을때의 환경 밖에서 호출되어도 그 환경에 접근할 수 있는 함수
    - 전역 변수의 사용을 억제 하기위해
    - 정보를 은닉하기 위해 
34. 코드 스플리팅
    - 하나의 큰 번들을 여러개의 작은 번들로 쪼개는 것
    - 필요한 번들만 로드 하여서 로딩 시간을 줄여줌.
    - 유저가 현재 필요하지 않은 코드는 로드 하지 않음으로써 앱의 성능이 크게 향상됨.
35. Memoization
    - 컴퓨터 프로그램이 동일한 계산을 반복해야 할 때 이전에 계산한 값을 메모리에 저장함으로써 동일
      한 계산의 반복 수행을 제거하여 프로그램 실행 속도를 빠르게 하는 기술
36. type, interface 차이
    - interface는 상속을 하지만 type은 상속을 하지않고 선언적 확장을 한다.
    - interface 속도가 더 빠르다
        - interface는 단순한 객체만 만든다
        - type은 재귀적으로 순회하면서 속성을 머지하는데 일부 never가 나오면서 제대로 머지가 되지 않는다.
37. function, arrow function 차이
    - function : this는 자신을 가장 마지막으로 품고 있는 scope로 항상 변한다.
    - arrow function : 처음 바인딩 된 스코프 안에서 가리키는 this가 절대 변하지 않는다.
38. 함수형 프로그래밍이란?
    - 함수형 프로그래밍은 거의 모든 것을 순수 함수로 나누어 문제를 해결하는 기법
        - 순수함수 : 부수 효과가 없는 함수
          함수 동일한 인자가 주어졌을 떄 항상 같은 값을 리턴하는 함수
    - 가독성을 높이고 유지보수가 쉽다.
39. Reflow Repaint 차이
    - Repaint : 화면에 변화가 있을 때 그리는 것
    - Reflow : 화면 구조가 변경되었을 떄 뷰포트 내에서 렌더 트리의 노드의 정확한 위치와 크기를 계산하는 과정
        - DOM 노드 추가 제거, DOM 노드 위치 변경, offset, scrollTop, scrollLeft와 같은 계산된 스타일 정보 요청 시 Reflow 발생
40. HTTP란? HTTP HTTPS 차이
    - HTTP : Client 요청이 있을 때만 서버가 응답하여 해당 정보를 전송하고 곧바로 연결을 종료하는 방식
    - 단방향적 통신으로, Server가 Cliend로 요청을 보낼 수는 없다.
    - HTTP 방식은 네트워크 상에서 정보를 누군가가 마음대로 열람, 수정이 가능하다. HTTPS는 열람 및 수정이 불가함.
41. 웹 표준
    - WWW측면을 서술하고 정의하는 공식 표준, 기술 규격을 가리키는 용어
    - 불필요한 소스와 팔일을 줄여 웹에 여유 공간을 확보해 페이지 로딩 속도를 빨리 할 수 있어 사용자에 더 나은 편의를 제공한다.
42. Restful API
    - HTTP URI를 통해 자원을 명시하고, HTTP Method를 통해 자원의 CRUD Operation을 적용하는 것을 의미한다.
    - 장점 
        - HTTP프로톨의 인프라를 사용해 별도의 인프라를 구축할 필요 없음
        - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능
        - 서버와 클라이언트의 역햘을 명확하게 분리
    - 단점 
        - 표준이 존재하지 않음
        - HTTP Method 형태가 제한적
        - 구형 브라우저가 아직 제대로 지원해주지 못한다 - PUT, DELETE


React 부분


1. React 동작 원리 Virtual DOM 설명
    - React는 실제로 DOM을 제어하는 방식이 아니라 가상의 DOM인 Virtual DOM을 두어 DOM을 직접 제어하지 않음으로 개발의 편의성을, 배치 처리로 DOM을 변경함으로 성능을 개선.
    - 이 때 Virtual DOM은 기존 DOM과의 변경 사항을 비교하여 실제 DOM에 필요한 최소한만 변경하여 효율성이 높음
    - Virtual DOM을 사용하지 않을 시에 DOM에 직접적인 변화가 생기면 렌더 트리 재생성 후 레이아웃 만드는 과정이 다시 반복되어서 비효율적이다.
2. Next.js 장점
    - 기본적으로 SSR을 제공
    - 코드 스플리팅 자동화
    - Express 같은 서버와 함께 구현가능
3. MobX를 사용한 이유
    - React를 위한 써드파티 state 관리 라이브러리 중에 Redux에서의 보일러플레이트 코드가 사라지고 데코레이터가 처리하기 때문에 깔끔한 코드가 생성됨.
    - State의 불변성을 유지하기 위해 다른 추가적인 라이브러리 사용 할 필요 없음.
4. Web pack 이 하는 역할
    - 여러 확장자, 파일로 나누어져 있는 파일들을 하나의 파일로 만들어주는 모듈 번들러 중 하나
    - 모듈 번들러는 여러개의 자바스크립트 파일을 하나의 파일로 묶어서 한 번의 요청을 통해 가지고 올 수 있게 함
    - 자바스크립트 코드를 압축하고 최적화 할 수 있어 로딩 속도를 높일 수 있음.
5. Babel
    - 최신 자바스크립트 문법을 모든 브라우저에서 사용할 수 있는 형태로 변환하는 역할을 하는 트랜스파일러.
6. JSX 란?
    - JSX는 HTML처럼 보이는 코드를 작성할 수 있게 해주는 자바스크립트 문법의 확장.
7. 제어 컴포넌트와 비제어 컴포넌트의 차이
    - form 엘리먼트 (select, textarea, input)에서 고유한 state를 유지함.
    - 제어 컴포넌트는 input값이 변경되면 input을 다시 렌더링 함.
8. React에서 Styling하는 보편적인 방식
    - 인라인 스타일링: 프로토타입을 만들 때 훌륭하지만 한계가 많다.
    - 클래스 기반 css 스타일: React에 익숙하지 않은 개발자들도 쉽게쉽게 스타일링이 가능하다
    - Css in JS 스타일링: 컴포넌트 안에서 스타일을 자바스크립트로 선언하여 스타일링 가능.
9. 클래스형 컴포넌트, 함수형 컴포넌트의 차이
    - 클래스형 컴포넌트는 hooks가 도입되기 이전 내부 state를 유지하거나 lifecycle을 활용하기 위해 클래스 기반의 컴포넌트를 사용했음.
    - 하지만 hooks가 도입 된 후 함수형 컴포넌트에서도 state와 lifecycle 등을 함수형에서도 사용할 수 있게 됨.
    - 오히려 함수형이 (this의 필요성이 사라짐, 공통 기능을 커스텀 hook으로 만들어서 재사용 하기 쉬워짐 등) 여러 이점이 있음.
    - 클래스형이 메모리 자원을 함수형 컴포넌트보다 조금 더 사용함.
10. Key 를 사용하는 이유
    - key는 collection을 렌더링할 때 Element와 데이터 사이 관계를 추적하기 쉽도록 반복되는 Element에 고유 key를 사용함.
    - key를 사용하지 않으면 collection에 item을 추가하거나 제거할 때 예상치 못한 동작 결과가 발생할 수 있음.
    - key는 고유한 ID를 사용하여야 하지만 마지막 수단으로 array index를 사용.
11. state와 props의 차이
    - props는 부모 컴포넌트에서 자식 컴포넌트로 전달되는 데이터로 자식 컴포넌트에서 수정할 수 없다.
    - state는 컴포넌트의 상태를 나타내며, 수정할 수 있다.
12. setState로 state를 변경하는 이유
    - 만약 state를 직접 변경하려고 시도한다면 리액트는 컴포넌트를 다시 렌더링 해야 하는지 알 수 없음. 그렇기에 setState를 사용하여 리액트가 컴포넌트의 UI를 업데이트 할 수 있게 함.
13. dynamic import
    - 정적인 module import 를 필요한 시점에 로드 할 수 있게 해줌.
    - Next.js의 dynamic import는 promise 과정을 거치지 않음.
14. React.lazy
    - 컴포넌트가 사용되는 시점에 가져오도록 구현 가능
    - 하지만 아무것도 없는 페이지가 노출 되었다가 로드 되어야지 화면이 표시됨.
    - Suspense를 이용하여 로딩화면 구현 가능
15. React.memo
    - 함수형 컴포넌트 적용되어 같은 props에 같은 렌더링 결과를 제공함.
    - props가 변경 되지 않는다면 다음 렌더링 때 메모이징 된 내용을 그대로 사용하게 됨.
16. useMemo
    - [] 안에 값이 바뀌었을 때만 다시 호출
    - useCallback과의 차이는 Callback은 함수를 반환, Memo는 값을 반환
    - Hook이기 때문에 오직 함수형 컴포넌트 안에서만 사용 가능하다 - React.memo랑 차이점
17. useEffect
    - async/await 을 직접적으로 사용하면 안됨
    - [] 안쓰면 렌더링 시, 쓰면 마운트 시
18. useReducer
    - 하나의 state를 여러가지 action 으로 변경 할 때 사용
    - redux랑 비슷
19. useRef
    - ref 객체 안에 current 속성이 실제 요소
    - createRef을 함수형에서 작성 시 렌더링마다 ref가 초기화 된다.
20. React의 최적화 방법
    - React.PureComponent - 이전 props와 state를 얇게 비교하여 Component 렌더링 횟수 감소
        - React.memo는 props만 비교
    - React.lazy 사용 
21. Redux란
    - Redux는 store라고 불리는 state 컨테이너 개념을 기반으로 하는데, store 컴포넌트는 데이터를 props로 받을 수 있음.
    - state를 변경하는 방법은 reducer를 통해 전달되는 store에 action을 보내는 것
22. Redux-Thunk VS Redux-Saga
    - 보일러 플레이트 코드량은 Redux-Thunk 가 더 적다.
    - 난이도는 Redux-Thunk가 더 쉽다.
    - 확장성은 Redux-Saga가 더 좋다. 
    - Redux-Saga가 순수함수를 유지한다.
    - Redux-Saga가 테스트가 쉽다.

