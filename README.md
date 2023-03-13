// 오리지널 리액트 방식
const root = document.getElementById("root");
const h3 = React.createElement(
  "h3",
  {
    id: "title",
    onMouseEnter: () => console.log("mouse enter"),
  },
  "I'll be a superstar."
);

const btn = React.createElement(
  "button",
  {
    onClick: () => console.log("클릭이 잘되네"),
  },
  "클릭하세요"
);

const container = React.createElement("div", null, [h3, btn]);
ReactDOM.render(container, root);

// JSX로 다시쓰기 : babel cdn추가, <script type="text/babel"> code </script>
const root2 = document.getElementById("root");
const Title = () => (
  <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
    리액트JS 시작
  </h3>
);

function Button() {
  return (
    <button
      className="click_btn"
      style={{ backgroundColor: "#8a7fea" }}
      onClick={() => console.log("클릭이 잘되네")}
    >
      클릭하세요
    </button>
  );
}
const Container = () => (
  <div>
    <Title />
    <Button />
  </div>
);

ReactDOM.render(<Container />, root);

// 다소 비효율적인 JSX 방식 : 각 Componenet마다 render를 빠지지않고 계속 써줘야하기때문
const root3 = document.getElementById("root");
let counter = 0;

function count() {
  counter = counter + 1;
  render();
}

function render() {
  ReactDOM.render(<Container />, root);
}

const Container2 = () => (
  <div>
    <h3>총 클릭 횟수 : {counter}</h3>
    <button onClick={count}>클릭하세요</button>
  </div>
);

render();

/* 리액트 배열 선언법 : 
    'hobby[0]'처럼 특색없이 표시하지 않기위해 선 배열선언 후 
     각 요소를 변수에 할당해 사용. data rendering에 사용할 방식이다. */
const hobby = ["bike", "workout", "reading", "listening"];
const [first, second, third, fourth] = hobby;
console.log(first, second, third, fourth);

function App() {
  /* data 배열 : [초기값, 값을 변환할 함수]로 선언된 배열 == React.useState()의 구조
            f의 자리에는 초기값을 바꿀때 사용할 함수를 넣는다. State는 함수안에 선언
            이 f(modifier)는 data가 바뀔때마다 Componenent를 재생성하고 UI를 리렌더링한다.
            물론 리액트기때문에 바뀌는 부분 {counter}만 리렌더링한다.
         */
  const data = React.useState(0);
  const [counter, modifier] = data;
  return (
    <div>
      <h3>총 클릭 횟수 : {counter}</h3>
      <button>클릭하세요</button>
    </div>
  );
}

ReactDOM.render(<App />, root);

// state를 변화시키는 두가지 방법 : 직접 값 할당, 함수 할당
const root4 = document.getElementById("root");

function App() {
  const [counter, setCounter] = React.useState(0);
  function countUp() {
    // setCounter(counter + 1);
    setCounter((current) => current + 1);
  }

  function reset() {
    setCounter(0);
  }
  return (
    <div>
      <h3>총 클릭 횟수 : {counter}</h3>
      <button onClick={countUp}>클릭하세요</button>&nbsp;
      <button onClick={reset}>초기화</button>
    </div>
  );
}

ReactDOM.render(<App />, root);