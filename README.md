# React


## 실습환경 구축

1. stackblitz: 환경 세팅 없이 Web에서 React 실행  
https://stackblitz.com/edit/react-wntue8rb?file=src%2FApp.js

2. NodeJs  
https://nodejs.org/ko/download  
LTS 설치 권장

3. VScode  
https://code.visualstudio.com/Download

4. VSCode  

- 상단바 Terminal > New Terminal > zsh Terminal 사용(일부 터미털에서 커멘드 동작 안함)
- ```npx create-react-app .```
- ```npm start``` 3000포트를 사용하는 웹앱이 실행됨(src/index.js 파일을 실행 시킴)

```npm (Node Package Manager): Node.js에서 사용하는 패키지 관리자```   
```npx (Node Package eXecute): npm과 함께 제공되는 실행 도구```  
</br></br>


## 소스코드 수정 방법

터미널에서 ctrl+c : 기존 개발환경 종료

```npm run buid```   
- 배포판을 생성
- 개발용 소스(src/)를 최적화된 정적 파일로 변환해서 build/ 폴더를 만든다. -> build/ 안에는 실제 서버에 올릴 수 있는 HTML, CSS, JS 파일만 남음.

```npx serve -s build```
- -s는 --single의 줄임말
- SPA(React, Vue 같은 Single Page App)에서 라우팅이 꼬이지 않도록, 모든 경로 요청을 index.html로 돌려준다.


크롬 개발자 도구 실행  
오른쪽 상단 점 3개(⋮) 클릭 →  도구 더보기 → 개발자 도구 선택 → 열린 창에서 Console 탭 클릭
</br></br>


## 컴포넌트(사용자 정의 태그) 만들기

- 컴포넌트(사용자 정의 태그)를 만들 때는 함수 사용한다. 이때 컴포넌트 명명법은 대문자로 시작하며, 소문자는 html 태그를 의미한다.
</br></br>


## props











</br></br>


## 이벤트
</br></br>
## state
</br></br>
## 생성 기능 구현
</br></br>
## 수정 기능 구현
</br></br>
## 삭제 기능 구현
