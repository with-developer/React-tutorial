# React-web
풀스택 개발자가 되기 위한 프로젝트   
저는 여태 Frontend는 `HTML + Javascript(JQuery) + CSS(Bootstrap 5.0)`를 사용해왔습니다.     
이 프로젝트는 React라는 새로운 Frontend Framework를 이해하기 위한 용도로 시작되었습니다.
original ref: https://ko.legacy.reactjs.org/tutorial/tutorial.html

## React란?
React는 웹 페이지나 앱의 사용자 인터페이스(UI)를 만들기 위한 JavaScript 라이브러리입니다.   
이 라이브러리를 사용하면 작은 부품(컴포넌트라고 부릅니다)을 만들어 큰 화면을 구성할 수 있습니다.   
각 컴포넌트는 독립적이고 재사용 가능하며, 이를 조합하여 복잡한 UI를 쉽게 만들 수 있습니다.   
React는 코드를 간결하고 이해하기 쉽게 만들어 줍니다.   

#### 그러면 컴포넌트란?
처음에는 `컴포넌트 == <div>`인가? 라는 생각을 했습니다.   
그래서 자료를 좀 찾아보니 컴포넌트는 단순히 `<div>`보다 더 큰 개념이었습니다.   
컴포넌트는 HTML, CSS, 그리고 JavaScript 로직을 포함할 수 있으며, 이를 하나의 독립적인, 재사용 가능한 단위로 묶어둔 것입니다.   
   
예를 들어, "버튼" 컴포넌트를 생각해보면:   
- HTML: 버튼을 구성하는 마크업 코드   
- CSS: 버튼의 스타일링   
- JavaScript: 버튼이 클릭됐을 때 어떤 동작을 해야 하는지   
이 모든 것을 하나의 "버튼 컴포넌트"로 정의할 수 있습니다.

이렇게 컴포넌트를 사용하면 코드의 재사용성이 높아지고, 유지보수가 쉬워집니다. 예를 들어 동일한 버튼 스타일이 여러 페이지에서 사용된다면, 그 버튼을 하나의 컴포넌트로 만들어 여러 곳에서 재사용할 수 있습니다.


## 환경 설정

1. node.js Download (version: 18.17.1)   
설치 완료 후 `npx -version` 명령어를 입력하면, `9.6.7` 버전을 사용중이라고 나옵니다.    
[Download Link](https://nodejs.org/en)

2. `npx create-react-app my-app` 명령을 실행하여 기본 프로젝트를 생성합니다.

3. 프로젝트가 생성되면 `/src` 경로에 여러가지 파일이 생성됩니다.   
해당 파일들을 다 삭제합니다.

4. `src/` 폴더에 `index.css`라는 파일을 생성하고 아래 CSS 코드를 추가해주세요.   
<details>
<summary>코드 접기/펼치기</summary>

```css
body {
    font: 14px "Century Gothic", Futura, sans-serif;
    margin: 20px;
}

ol,
ul {
    padding-left: 30px;
}

.board-row:after {
    clear: both;
    content: "";
    display: table;
}

.status {
    margin-bottom: 10px;
}

.square {
    background: #fff;
    border: 1px solid #999;
    float: left;
    font-size: 24px;
    font-weight: bold;
    line-height: 34px;
    height: 34px;
    margin-right: -1px;
    margin-top: -1px;
    padding: 0;
    text-align: center;
    width: 34px;
}

.square:focus {
    outline: none;
}

.kbd-navigation .square:focus {
    background: #ddd;
}

.game {
    display: flex;
    flex-direction: row;
}

.game-info {
    margin-left: 20px;
}
```
</details>

5. `src/` 폴더에 `index.js`라는 파일을 생성하고 아래 JS 코드를 추가해주세요.

<details>
<summary>코드 접기/펼치기</summary>

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';

class Square extends React.Component {
    render() {
        return (
            <button className="square">
                {/* TODO */}
            </button>
        );
    }
}

class Board extends React.Component {
    renderSquare(i) {
        return <Square />;
    }

    render() {
        const status = 'Next player: X';

        return (
            <div>
                <div className="status">{status}</div>
                <div className="board-row">
                    {this.renderSquare(0)}
                    {this.renderSquare(1)}
                    {this.renderSquare(2)}
                </div>
                <div className="board-row">
                    {this.renderSquare(3)}
                    {this.renderSquare(4)}
                    {this.renderSquare(5)}
                </div>
                <div className="board-row">
                    {this.renderSquare(6)}
                    {this.renderSquare(7)}
                    {this.renderSquare(8)}
                </div>
            </div>
        );
    }
}

class Game extends React.Component {
    render() {
        return (
            <div className="game">
                <div className="game-board">
                    <Board />
                </div>
                <div className="game-info">
                    <div>{/* status */}</div>
                    <ol>{/* TODO */}</ol>
                </div>
            </div>
        );
    }
}

// ========================================

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<Game />);
```
</details>

6. `npm start` 명령을 실행하고 브라우저에서 `http://localhost:3000`를 열면 비어있는 틱택토 필드를 확인할 수 있습니다.

## 기본 코드 분석
1. `src/index.js`
코드를 살펴보면 3개의 컴포넌트가 존재합니다.
- Square: \<button>을 렌더링하기 위한 용도
- Board: 9개의 사각형을 렌더링하기 위한 용도
- Game: 게임 판을 렌더링하기 위한 용도

## Props를 통해 데이터 전달하기

#### Props는 또 뭐지?
`Flask의 Jinja2 Template Engine`, `Django의 Django Template Engine`, `Node.js의 EJS` 등을 사용해본 저에게 Props는 Backend에서 Frontend에게 데이터를 return 해주고, Frontend에서 `{{ variable }}` 처럼 출력시켜주는 것과 비슷하다고 느껴졌습니다.   

props는 React에서 컴포넌트 간에 데이터를 전달하는 방법 중 하나입니다. props는 "properties"의 약자로, HTML의 태그에서 속성(attribute)을 설정하는 것과 유사한 방식으로 작동합니다.

예를 들어, 사용자의 이름을 출력하는 간단한 "환영 메시지" 컴포넌트가 있다고 가정해봅시다. 이 컴포넌트는 사용자의 이름을 props를 통해 받을 수 있습니다.   
```javascript
// WelcomeMessage 컴포넌트 정의
function WelcomeMessage(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// WelcomeMessage 컴포넌트 사용
<WelcomeMessage name="John" />
```
위의 예에서 name="John"이라고 설정하면, WelcomeMessage 컴포넌트 내부의 props.name은 "John"이 됩니다. 결과적으로 화면에는 "Hello, John!"이 출력됩니다.

---
1. `/src/index.js` 파일의 Board 클래스를 아래와 같이 수정합니다.
```javascript
class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i} />;
  }
}
```

2. `/src/index.js` 파일의 Square 클래스를 아래와 같이 수정합니다.
```javascript
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}
```
[변경 전]
![변경 전](/README_images/1.png)

[변경 후]
![변경 후](/README_images/2.png)

위처럼 각 네모박스 내부에 0부터 8까지의 숫자가 출력되었습니다.
저도 아직 정확하게 이해한 것은 아니지만, 제가 이해한 내용은 다음과 같습니다.

1. index.html에서 `<div id="root"></div>` 태그에 의해 아래 코드가 실행됩니다.
```javascript
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<Game />);
```
2. Game 컴포넌트를 render 하기 때문에 `<div id="root">` 태그 내부에서 아래의 코드가 실행됩니다.
```javascript
class Game extends React.Component {
    render() {
        return (
            <div className="game">
                <div className="game-board">
                    <Board />
                </div>
                <div className="game-info">
                    <div>{/* status */}</div>
                    <ol>{/* TODO */}</ol>
                </div>
            </div>
        );
    }
}
```
3. Game 컴포넌트에서는 Board 컴포넌트를 다시 호출합니다.
```javascript
class Board extends React.Component {
    renderSquare(i) {
        return <Square value={i} />;
    }

    render() {
        const status = 'Next player: X';

        return (
            <div>
                <div className="status">{status}</div>
                <div className="board-row">
                    {this.renderSquare(0)}
                    {this.renderSquare(1)}
                    {this.renderSquare(2)}
                </div>
                <div className="board-row">
                    {this.renderSquare(3)}
                    {this.renderSquare(4)}
                    {this.renderSquare(5)}
                </div>
                <div className="board-row">
                    {this.renderSquare(6)}
                    {this.renderSquare(7)}
                    {this.renderSquare(8)}
                </div>
            </div>
        );
    }
}
```
4. Board 컴포넌트에서는 `this.renderSquare(숫자)`를 통해 Sqaure 컴포넌트를 다시 호출합니다.
```javascript
class Square extends React.Component {
    render() {
        return (
            <button className="square">
                {this.props.value}
            </button>
        );
    }
}
```

위 과정을 통해 각 네모 박스에 0부터 8까지의 숫자가 담긴 네모 버튼이 생성된 것입니다.
Jinja2, EJS 처럼 react에서도 for문을 통해 요소를 생성할 수 있다면, 더 간결한 코드로 작성할 수 있어 보입니다.   
아직 이 부분은 튜토리얼에 없기 때문에 넘어가도록 하겠습니다.

## 사용자와 상호작용하는 컴포넌트 만들기
1. Square 컴포넌트를 클릭하면 `X`가 표시되도록 수정하려고 합니다.
우선 button에 onclick 기능을 추가하여 console.log에 버튼이 클릭되었는지 로그로 남겨보겠습니다.
```javascript
// File Path to "/src/index.js"
class Square extends React.Component {
    render() {
        return (
            <button className="square" onClick={function(){console.log('click square');}}>
                {this.props.value}
            </button>
        );
    }
}
```
위 코드에서 중요한 부분은 `onClick={function() { console.log('click square'); }}`가 아닌, `onClick={() => console.log('click square')}`형식으로 코드를 작성해야 한다는 점 입니다.   
전자대로 코드를 작성한다면, 페이지를 새로고침 하더라도 console.log가 그대로 남아있게 되기 때문입니다.