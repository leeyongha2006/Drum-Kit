# Drum-Kit
JavaScript를 사용하여 드럼키트 만들기
![image](https://github.com/leeyongha2006/Drum-Kit/assets/126844590/5c049c4d-c101-4d6c-90aa-6c1c23a86010)

### 키보드나 마우스를 입력하여 드럼 소리를 내는 프로그램이다. 
## javascript
```javascript
const keys = Array.from(document.querySelectorAll('.key'));

// 2. 키 코드 사전 정의 (Define key code dictionary)
const keyCode = {
  A: 65,
  S: 83,
  D: 68,
  F: 70,
  G: 71,
  H: 72,
  J: 74,
  K: 75,
  L: 76,
};

// 3. 변형 애니메이션 종료 시 처리 함수 (Function to handle transition end)
function removeTransition(e) {
  if (e.propertyName !== 'transform') return; // 변형 애니메이션이 아니라면 리턴 (If not a transform animation, return)
  e.target.classList.remove('playing'); // 클래스 'playing' 제거 (Remove class 'playing')
}

// 4. 키 누르기 이벤트 처리 함수 (Function to handle keydown event)
function playSound(e) {
  // 키 코드 또는 키 글자에 해당하는 데이터 속성을 가진 오디오 요소 찾기
  // (Find audio element with data attribute matching key code or key content)
  const audio = document.querySelector(
    `audio[data-key="${e.keyCode || keyCode[e.target.innerHTML]}"]`
  );

  // 키 요소 (div) 찾기
  // (Find the key element (div))
  const key = document.querySelector(
    `div[data-key="${e.keyCode || keyCode[e.target.innerHTML]}"]`
  );

  if (!audio) return; // 오디오 요소가 없으면 리턴 (If no audio element found, return)

  key.classList.add('playing'); // 클래스 'playing' 추가 (Add class 'playing')
  audio.currentTime = 0; // 재생 시간 초기화 (Reset playback time)
  audio.play(); // 오디오 재생 (Play audio)
}

// 5. 모든 키 요소에 변형 애니메이션 종료 이벤트 리스너 등록
// (Add transitionend event listener to all key elements)
keys.forEach((key) => key.addEventListener('transitionend', removeTransition));

// 6. window 객체에 키 누름 이벤트 리스너 등록
// (Add keydown event listener to window object)
window.addEventListener('keydown', playSound);

// 7. 모든 키 요소에 클릭 이벤트 리스너 등록
// (Add click event listener to all key elements)
keys.forEach((key) =>
  key.addEventListener('click', (e) => {
    playSound(e);
  })
);
```
## index.html

```html

<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>Drum Kit</title>
  <link rel="stylesheet" href="css/style.css">
</head>

<body>
  <h1 id="title">Drum Kit</h1>
  <div class="keys">
    <div data-key="65" class="A key">
      <kbd>A</kbd>
      <span class="sound">clap</span>
    </div>
    <div data-key="83" class="S key">
      <kbd>S</kbd>
      <span class="sound">hihat</span>
    </div>
    <div data-key="68" class="D key">
      <kbd>D</kbd>
      <span class="sound">kick</span>
    </div>
    <div data-key="70" class="F key">
      <kbd>F</kbd>
      <span class="sound">openhat</span>
    </div>
    <div data-key="71" class="G key">
      <kbd>G</kbd>
      <span class="sound">boom</span>
    </div>
    <div data-key="72" class="H key">
      <kbd>H</kbd>
      <span class="sound">ride</span>
    </div>
    <div data-key="74" class="J key">
      <kbd>J</kbd>
      <span class="sound">snare</span>
    </div>
    <div data-key="75" class="K key">
      <kbd>K</kbd>
      <span class="sound">tom</span>
    </div>
    <div data-key="76" class="L key">
      <kbd>L</kbd>
      <span class="sound">tink</span>
    </div>
  </div>

  <audio data-key="65" src="sounds/clap.wav"></audio>
  <audio data-key="83" src="sounds/hihat.wav"></audio>
  <audio data-key="68" src="sounds/kick.wav"></audio>
  <audio data-key="70" src="sounds/openhat.wav"></audio>
  <audio data-key="71" src="sounds/boom.wav"></audio>
  <audio data-key="72" src="sounds/ride.wav"></audio>
  <audio data-key="74" src="sounds/snare.wav"></audio>
  <audio data-key="75" src="sounds/tom.wav"></audio>
  <audio data-key="76" src="sounds/tink.wav"></audio>
  <script src="script/main.js"></script>
</body>
</html>
```
## style.css
```css
body,
html {
  margin: 0;
  padding: 0;
  font-family: 'sans';
  font-size: 10px;
  background: #19172e;
  user-select: none;
}

@font-face {
  src: url('font/sans.ttf');
  font-family: 'sans';
}

h1 {
  font-size: 5.5rem;
  color: #FEFFE2;
  font-family: "Arvo", cursive;
  text-align: center;
}

span {
  font-weight: 100;
}

.keys {
  display: flex;
  flex: 1;
  min-height: 40vh;
  align-items: center;
  justify-content: center;
}

.key {
  border: .4rem solid white;
  border-radius: .5rem;
  margin: 1rem;
  font-size: 1.5rem;
  padding: 1rem .5rem;
  transition: all .07s ease;
  width: 10rem;
  text-align: center;
  color: white;
  background-color: #212121;
}

.playing {
  transform: scale(1.1);
  border-color: #bb86fc;
  box-shadow: 0 0 1rem #bb86fc;
}

kbd {
  display: block;
  font-size: 4rem;
}

.sound {
  font-size: 1.2rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: .1rem;
  color: #bb86fc;
}

kbd {
  cursor: pointer;
}
```
