# React


[1. 실습환경구축](#실습환경-구축)  
[2. 소스코드 수정 방법](#소스코드-수정-방법)  
[3. 컴포넌트 만들기](#컴포넌트-만들기)  
[4. props](#props)   
[5. 이벤트  ](#이벤트)  
[6. state ](#state)    
[7. 생성 기능 구현](#생성-기능-구현)  
[8. 수정 기능 구현](#수정-기능-구현)  
[9. 삭제 기능 구현](#삭제-기능-구현)   
</br></br>


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
- ```npx create-react-app my-app```  or  ```npx create-react-app .```   
     ** '허가되지 않은 스크립트 관련 에러'
   - (Window)Windows PowerShell > 우클릭 관리자 권한으로 실행 > Set-ExecutionPolicy Unrestricted
   - (Mac)sudo npx create-react-app my app
  
- ```npm start``` 3000포트를 사용하는 웹앱이 실행됨(src/index.js 파일을 실행 시킴)

   - npm (Node Package Manager): Node.js에서 사용하는 패키지 관리자   
   - npx (Node Package eXecute): npm과 함께 제공되는 실행 도구
   - JSX: JavaScript 안에서 HTML과 비슷한 문법을 사용할 수 있게 해주는 문법 확장. React의 Javascript 에서 return 해주고 있는 것은 html이 아니라 JSX임

</br></br>


## 소스코드 수정 방법
1. ```터미널에서 ctrl+c```
   - 기존 개발환경 종료

2. ```npm run buid```   
   - 배포판을 생성
   - 개발용 소스(src/)를 최적화된 정적 파일로 변환해서 build/ 폴더를 만든다. -> build/ 안에는 실제 서버에 올릴 수 있는 HTML, CSS, JS 파일만 남음.

3. ```npx serve -s build```
   - -s는 --single의 줄임말
   - SPA(React, Vue 같은 Single Page App)에서 라우팅이 꼬이지 않도록, 모든 경로 요청을 index.html로 돌려준다.
</br></br>


## 컴포넌트 만들기
- 컴포넌트(사용자 정의 태그)를 만들 때는 함수 사용한다. 이때 컴포넌트 명명법은 대문자로 시작하며, 소문자는 html 태그를 의미한다.
</br></br>


## props  
- 컴포넌트의 입력값(속성)인 props
- 컴포넌트에 외부에서 값을 전달하는 방법
- 읽기 전용 (immutable): 자식 컴포넌트는 props를 직접 수정할 수 없다.

```javascript
// props 예시
// 1.부모 → 자식 데이터 전달
function Header(props){
  console.log('props', props, props.title);
  return <header>
    <h1><a href="/">{props.title}</a></h1>
  </header>
}

<Header title="WEB"></Header>

// 2.기본값 설정
function Greeting({ name = "손님" }) {
  return <h1>Hello, {name}!</h1>;
}

// 3.구조 분해 할당
function Greeting({ name, age }) {
  return <p>{name} is {age} years old.</p>;
}
```
</br></br>


## 이벤트
- “사용자가 웹 화면에서 뭘 했을 때, 우리 코드가 어떻게 반응할지”를 정의하는 장치
```javascript
function Header(props){
  return <header>
    <h1><a href="/" onClick={(event)=>{
      event.preventDefault(); //<a>의 기본 동작을 방지
      props.onChangeMode();
    }}>{props.title}</a></h1>
  </header>
}

<Header title="WEB" onChangeMode={()=>{
  alert('Header');
}}></Header>

``` 
</br></br>


## state  
- 컴포넌트가 가지고 있는 동적인 데이터(변하는 값)를 저장하는 객체
- 한 번 렌더링된 후에도 사용자 입력, 네트워크 응답, 내부 로직 등에 따라 값이 바뀔 수 있는 데이터들을 관리할 때 사용
- Destructuring 문법   
   - 배열이나 객체의 값을 쉽게 꺼내서 변수에 담을 수 있는 문법
   - 긴 코드를 짧고 직관적으로 줄여주기 때문에 리액트에서 props, state를 다룰 때 자주 사용   
   - e.g. let [a, c] = [1, 2];   

```javascript
import React, { useState } from "react";

function Counter() {
  // count: 현재 값, setCount: 값을 바꾸는 함수
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>현재 값: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        +1 증가
      </button>
    </div>
  );
}
```
</br></br>


## 생성 기능 구현
```javascript
import {useState} from 'react';

function Create(props){
  return <article>
    <h2>Create</h2>
    <form onSubmit={event=>{
      event.preventDefault();
      const title = event.target.title.value;
      const body = event.target.body.value;
      props.onCreate(title, body);
    }}>
      <p><input type="text" name="title" placeholder="title"/></p>
      <p><textarea name="body" placeholder="body"></textarea></p>
      <p><input type="submit" value="Create"></input></p>
    </form>
  </article>
}

function App() {
  const [id, setId] = useState(null);

  const [nextId, setNextId] = useState(4);

  const [topics, setTopics] = useState([
    {id:1, title:'html', body:'html is ...'},
    {id:2, title:'css', body:'css is ...'},
    {id:3, title:'javascript', body:'javascript is ...'}
  ]);

  return <Create onCreate={(_title, _body)=>{
      const newTopic = {id:nextId, title:_title, body:_body}
      const newTopics = [...topics]
      newTopics.push(newTopic);
      setTopics(newTopics);
      setMode('READ');
      setId(nextId);
      setNextId(nextId+1);
    }}></Create> 
}

```
</br></br>


## 수정 기능 구현
```javascript
function Update(props){
  const [title, setTitle] = useState(props.title);
  const [body, setBody] = useState(props.body);
  return <article>
    <h2>Update</h2>
    <form onSubmit={event=>{
      event.preventDefault();
      const title = event.target.title.value;
      const body = event.target.body.value;
      props.onUpdate(title, body);
    }}>
      <p><input type="text" name="title" placeholder="title" value={title} onChange={event=>{
        setTitle(event.target.value);
      }}/></p>
      <p><textarea name="body" placeholder="body" value={body} onChange={event=>{
        setBody(event.target.value);
      }}></textarea></p>
      <p><input type="submit" value="Update"></input></p>
    </form>
  </article>
}

function App() {
   const [id, setId] = useState(null);

   const [topics, setTopics] = useState([
     {id:1, title:'html', body:'html is ...'},
     {id:2, title:'css', body:'css is ...'},
     {id:3, title:'javascript', body:'javascript is ...'}
   ]);

    let title, body = null;

    for(let i=0; i<topics.length; i++){
      if(topics[i].id === id){
        title = topics[i].title;
        body = topics[i].body;
      }
    }

    return <Update title={title} body={body} onUpdate={(title, body)=>{
      console.log(title, body);
      const newTopics = [...topics]
      const updatedTopic = {id:id, title:title, body:body}

      for(let i=0; i<newTopics.length; i++){
        if(newTopics[i].id === id){
          newTopics[i] = updatedTopic;
          break;
        }
      }
      setTopics(newTopics);
    }}></Update>   
}
```
</br></br>


## 삭제 기능 구현
```javascript
fun App() {
   const [topics, setTopics] = useState([
     {id:1, title:'html', body:'html is ...'},
     {id:2, title:'css', body:'css is ...'},
     {id:3, title:'javascript', body:'javascript is ...'}
   ]);   

   return <>
      <li><a href={'/update/'+id} onClick={event=>{
        event.preventDefault();
        setMode('UPDATE');
      }}>Update</a></li>

      <li><input type="button" value="Delete" onClick={()=>{
        const newTopics = []
        for(let i=0; i<topics.length; i++){
          if(topics[i].id !== id){
            newTopics.push(topics[i]);
          }
        }
        setTopics(newTopics);
      }} /></li>
    </>
}
```
</br></br>


## JSX 문법
1. class 넣을 땐 `className`   
2. 변수 넣을 땐 `{중괄호}` 사용
3. style 넣을 땐 `style={ {스타일명:'값'} }`   
   e.g. style={ {color : 'red', fontSize: '16px'} } * font-size 처럼 - 기호 사용 금지: '-'은 javascript 에서 '뺄셈'기능

## Javascript 문법   
1. 함수 만드는 문법 `()=>{}` e.g. `<span onClick={ () => { console.log(1) } }> Like </span>`





