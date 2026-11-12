[README.md](https://github.com/user-attachments/files/34724033/README.md)
# 3D 디지털 트윈 프로젝트 실행 및 코드 구조 분석

## 1. 문서 개요

이 문서는 다음 두 HTML 파일의 실제 코드 구조를 바탕으로 작성했습니다.

- `smart_classroom_camera_stable(5).html` — 스마트 학교 교실 디지털 트윈
- `ThreeJS_korean_bus.html` — 한국형 전기 시내버스 스마트팩토리 디지털 트윈

두 파일은 HTML 안에 CSS와 JavaScript를 함께 작성한 **단일 HTML 파일형 Three.js 웹 애플리케이션**입니다. 별도의 빌드 도구나 프레임워크를 사용하는 구조는 아니며, Three.js 라이브러리와 OrbitControls를 CDN으로 불러옵니다.

> 두 프로젝트의 센서 값, 공정 상태, 품질 상태 등은 코드에서 계산·표시하는 교육용 시뮬레이션 데이터입니다. 실제 교실 센서, 실제 공장 설비, 실제 제조사의 생산 시스템이나 검사 장비에 연결된 것은 아닙니다.

---

## 2. 두 프로젝트의 주요 기능

### 2.1 스마트 학교 교실

교실의 구조와 가구를 Three.js로 생성하고, 가상의 환경 센서 값과 설비 제어를 연결한 디지털 트윈 예제입니다.

주요 기능:

- 실사풍을 목표로 한 교실 3D 공간과 가구의 절차적 생성
- 학생 모델, 전자칠판, 창문, 블라인드, 조명, 공조 설비 등의 표현
- 실내 온도, CO₂, 조도, 재실 인원 표시
- 재실 인원, 자연광, 목표 온도, 환기, LED 조명, 블라인드 조절
- 수업 중, 쉬는 시간, 집중 환기, 야간 소등 시나리오
- 교실 전체, 학생, 전자칠판, 창가, 평면 조망 카메라 전환
- 센서 라벨과 학생 모델 표시 전환
- 장면 JSON, 센서 CSV, 3D 화면 PNG 내보내기
- WebGL 컨텍스트 손실 및 초기 로딩 실패 안내

교실의 주요 센서·상태 데이터는 JavaScript의 시뮬레이션 상태 객체에서 관리됩니다. 실제 IoT 장치나 서버에서 값을 수신하는 코드는 아닙니다.

### 2.2 한국형 전기버스 스마트팩토리

전기 시내버스의 부품과 조립 과정을 Three.js로 구성하고, 8단계 공정 진행을 체험하도록 만든 교육용 디지털 트윈입니다.

주요 기능:

- 공장 바닥, 건축 구조, 조명, 설비, 로봇 등 공장 장면 구성
- 전기버스의 프레임, 바퀴, 배터리, 차체, 외판, 유리, 도어, 실내 구조 표현
- 8단계 조립 공정 선택 및 자동 실행
- 이전·다음 단계 이동과 초기화
- 간선·지선·광역·순환 계열의 차체 색상 변경
- 부품 클릭 시 부품 설명 표시
- X-RAY 반투명 모드
- 분해 보기와 조립 상태 복원
- 도어 열기, 카메라 자동 회전, 시점 초기화
- 사선 전경, 측면, 전면, 후면, 실내, 상부, 하부 카메라 시점
- 현재 3D 화면 PNG 저장 및 도움말 대화상자

공정 순서와 부품은 교육용 개념 모델입니다. 실제 제조사의 공정 순서, 부품 치수, 설비 및 품질 인증을 정밀하게 재현하지 않습니다.

---

## 3. 실행 방법

### 3.1 가장 권장하는 방법: VS Code Live Server

두 파일 모두 JavaScript의 ES Module 문법(`type="module"`)과 import map을 사용합니다. 따라서 HTML 파일을 더블클릭해 `file://` 주소로 실행하면 브라우저의 보안 정책(CORS 등) 때문에 모듈을 불러오지 못할 수 있습니다.

1. 두 HTML 파일을 한 폴더에 저장합니다.
2. Visual Studio Code에서 해당 폴더를 엽니다.
3. Extensions에서 **Live Server**를 설치합니다.
4. 실행할 HTML 파일을 마우스 오른쪽 버튼으로 클릭합니다.
5. **Open with Live Server**를 선택합니다.
6. Chrome 또는 Edge에서 3D 장면이 표시되는지 확인합니다.

예를 들어 브라우저 주소는 다음과 같은 형태가 됩니다.

```text
http://127.0.0.1:5500/smart_classroom_camera_stable(5).html
http://127.0.0.1:5500/ThreeJS_korean_bus.html
```

실제 포트 번호와 주소는 Live Server 설정에 따라 달라질 수 있습니다.

### 3.2 Python 로컬 서버로 실행

Python이 설치되어 있다면 별도 확장 프로그램 없이 실행할 수 있습니다.

1. 두 HTML 파일이 들어 있는 폴더를 엽니다.
2. 해당 폴더에서 터미널을 실행합니다.
3. 다음 명령어를 입력합니다.

```bash
python -m http.server 8000
```

4. 브라우저에서 아래 주소로 접속합니다.

```text
http://localhost:8000/smart_classroom_camera_stable(5).html
http://localhost:8000/ThreeJS_korean_bus.html
```

서버를 종료하려면 터미널에서 `Ctrl + C`를 누릅니다.

### 3.3 GitHub Pages로 배포

두 파일을 GitHub 저장소의 최상위(root)에 업로드합니다.

```text
repository/
├── index.html                         # 프로젝트 선택 메인 화면(사용하는 경우)
├── smart_classroom_camera_stable(5).html
└── ThreeJS_korean_bus.html
```

`index.html`을 메인 화면으로 사용한다면 링크의 파일명과 실제 업로드한 파일명이 정확히 일치해야 합니다.

예시:

```html
<a href="./smart_classroom_camera_stable(5).html">스마트 교실 실행</a>
<a href="./ThreeJS_korean_bus.html">전기버스 공장 실행</a>
```

GitHub 저장소에서 **Settings → Pages → Deploy from a branch → main → /(root) → Save** 순서로 설정합니다. 배포가 완료되면 GitHub Pages 주소로 접속합니다.

### 3.4 실행 환경 체크리스트

- 인터넷 연결: CDN에서 Three.js 모듈을 내려받기 위해 필요
- 브라우저: 최신 Chrome 또는 Edge 권장
- 그래픽 가속: WebGL 사용 가능 상태여야 함
- 실행 방식: `file://` 더블클릭보다 Live Server, Python 서버, GitHub Pages 권장
- 화면 크기: 두 파일 모두 반응형 CSS가 있으나, 3D 조작은 데스크톱에서 더 편리함
- 성능: 그림자, 다수의 3D 메시, 애니메이션으로 인해 저사양 기기에서는 프레임 저하가 발생할 수 있음

---

## 4. 전체 코드의 공통 문법 구조

두 파일은 다음과 같은 HTML 문서 구조를 공유합니다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <!-- 문자 인코딩, 화면 크기, 페이지 제목 -->
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>페이지 제목</title>

  <!-- 화면 디자인 -->
  <style>
    /* CSS */
  </style>

  <!-- Three.js 모듈 경로 지정 -->
  <script type="importmap">
    {
      "imports": {
        "three": "Three.js 모듈 URL",
        "three/addons/": "Three.js 추가 모듈 URL"
      }
    }
  </script>
</head>
<body>
  <!-- 화면에 표시되는 HTML 요소 -->
  <div id="stage"></div>

  <!-- Three.js와 애플리케이션 동작 코드 -->
  <script type="module">
    import * as THREE from 'three';
    import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

    // 3D 장면과 UI 제어 코드
  </script>
</body>
</html>
```

실제 두 파일은 이 기본 구조를 각 프로젝트에 맞게 확장한 형태입니다. 교실 파일은 별도의 JSON 장면 사양과 초기 오류 처리 스크립트도 포함합니다.

### 4.1 HTML: 화면의 뼈대

HTML은 화면에 표시할 요소와 각 요소의 식별자를 정의합니다.

주요 문법:

| 문법 | 역할 |
|---|---|
| `<!DOCTYPE html>` | HTML5 문서 선언 |
| `<html lang="ko">` | 한국어 문서 지정 |
| `<head>` | 문서 설정과 CSS, 모듈 설정 |
| `<meta>` | 문자 인코딩, 반응형 화면 등 설정 |
| `<title>` | 브라우저 탭 제목 |
| `<body>` | 실제 화면에 표시되는 내용 |
| `<div>` | 화면 요소를 묶는 컨테이너 |
| `<aside>` | 보조 패널 |
| `<main>` | 주요 콘텐츠 |
| `<button>` | 사용자 조작 버튼 |
| `<input>` | 사용자 입력 |
| `<canvas>` | 그래픽 또는 2D 차트 표시 영역 |
| `id` | JavaScript가 특정 HTML 요소를 찾는 식별자 |
| `class` | CSS 스타일을 적용하는 분류 이름 |

예를 들어 다음 HTML은 JavaScript에서 `stage`라는 이름으로 찾아 Three.js 렌더링 화면을 삽입할 공간입니다.

```html
<div id="stage"></div>
```

버스 파일에서는 다음 요소가 3D 화면을 담는 컨테이너입니다.

```html
<div id="world"></div>
```

### 4.2 CSS: 화면 디자인과 배치

CSS는 HTML 요소의 크기, 위치, 색상, 글꼴, 반응형 레이아웃을 담당합니다.

두 파일 모두 `<style>` 태그 안에 CSS를 작성합니다.

주요 문법:

```css
/* 전체 요소의 크기 계산 방식 */
* {
  box-sizing: border-box;
}

/* 화면 전체 */
html, body {
  margin: 0;
  height: 100%;
}

/* ID 선택자 */
#stage {
  position: fixed;
  inset: 0;
}

/* 클래스 선택자 */
.control-panel {
  position: absolute;
  right: 22px;
  width: 334px;
}

/* 반응형 화면 */
@media (max-width: 780px) {
  .control-panel {
    width: auto;
  }
}
```

| CSS 문법 | 설명 |
|---|---|
| `#이름` | 특정 ID를 가진 요소 선택 |
| `.이름` | 특정 클래스를 가진 요소 선택 |
| `position` | 요소의 위치 지정 |
| `display: grid` | 격자형 배치 |
| `display: flex` | 유연한 일렬 배치 |
| `width`, `height` | 너비와 높이 |
| `margin`, `padding` | 바깥쪽·안쪽 여백 |
| `background` | 배경색 또는 배경 효과 |
| `border-radius` | 모서리 둥글기 |
| `z-index` | 요소의 앞뒤 표시 순서 |
| `@media` | 화면 크기 등에 따른 반응형 스타일 |
| `:hover` | 마우스를 올렸을 때의 스타일 |

교실 파일은 청록색 계열의 어두운 패널 UI를, 버스 파일은 파란색 계열의 공장 관제 UI를 사용합니다.

### 4.3 Import Map: 외부 라이브러리 경로

두 파일은 `importmap`을 사용해 모듈 이름과 CDN 주소를 연결합니다.

교실 파일:

```html
<script type="importmap">
{
  "imports": {
    "three": "https://cdn.jsdelivr.net/npm/three@0.164.1/build/three.module.js",
    "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.164.1/examples/jsm/"
  }
}
</script>
```

버스 파일:

```html
<script type="importmap">
{
  "imports": {
    "three": "https://cdn.jsdelivr.net/npm/three@0.180.0/build/three.module.js",
    "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.180.0/examples/jsm/"
  }
}
</script>
```

두 프로젝트는 서로 다른 Three.js 버전을 사용합니다.

- 교실: Three.js `0.164.1`
- 버스: Three.js `0.180.0`

`three`는 핵심 라이브러리 경로이고, `three/addons/`는 OrbitControls 같은 추가 모듈 경로입니다.

### 4.4 JavaScript ES Module

두 파일의 3D 코드는 다음과 같이 모듈을 불러옵니다.

```javascript
import * as THREE from 'three';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
```

- `import`: 다른 모듈에서 기능을 가져오는 문법
- `THREE`: Three.js의 여러 클래스와 기능을 묶어 사용하는 별칭
- `OrbitControls`: 마우스로 카메라를 회전·확대·이동시키는 컨트롤
- `type="module"`: 브라우저가 JavaScript를 ES Module 방식으로 실행하도록 지정

따라서 이 코드는 일반적인 `<script>`가 아니라 `<script type="module">` 안에 있어야 합니다.

### 4.5 JavaScript의 기본 문법

두 프로젝트에서 반복적으로 사용하는 문법입니다.

**상수와 변수**

```javascript
const scene = new THREE.Scene();
let renderer;
```

- `const`: 다시 다른 값으로 대입하지 않을 변수를 선언
- `let`: 이후 값이 바뀔 수 있는 변수를 선언

**함수**

```javascript
function setView(id) {
  // 카메라 시점 변경
}
```

기능을 하나의 단위로 묶어 필요할 때 실행합니다.

**화살표 함수**

```javascript
const $ = id => document.getElementById(id);
```

HTML 요소를 ID로 찾는 짧은 함수입니다. 이후 `$('world')`처럼 사용합니다.

**객체**

```javascript
const config = {
  occupancy: 18,
  ventilation: 58
};
```

관련된 데이터를 이름과 값의 쌍으로 묶습니다.

**배열**

```javascript
const values = [10, 20, 30];
```

여러 데이터를 순서대로 저장합니다.

**조건문**

```javascript
if (renderer) {
  // 렌더러가 준비된 경우
} else {
  // 준비되지 않은 경우
}
```

**반복문**

```javascript
for (const item of items) {
  // 배열의 항목을 순서대로 처리
}
```

**이벤트 리스너**

```javascript
button.addEventListener('click', () => {
  // 버튼 클릭 시 실행
});
```

사용자의 클릭, 입력, 키보드 조작 등의 이벤트에 반응합니다.

**템플릿 문자열**

```javascript
const message = `현재 단계: ${step}`;
```

백틱(`) 안에서 `${변수}` 형태로 값을 문자열에 삽입합니다.

---

## 5. Three.js 3D 엔진 구조

두 프로젝트의 핵심은 Three.js가 브라우저의 WebGL을 이용해 3D 장면을 렌더링한다는 점입니다.

일반적인 처리 흐름은 다음과 같습니다.

```text
HTML 컨테이너
    ↓
Three.js 모듈 불러오기
    ↓
Scene 생성
    ↓
Camera 생성
    ↓
Renderer 생성
    ↓
Geometry + Material 생성
    ↓
Mesh 또는 Group 구성
    ↓
Scene에 객체 추가
    ↓
OrbitControls 연결
    ↓
애니메이션 / 렌더링 반복
```

### 5.1 Scene: 3D 공간

```javascript
const scene = new THREE.Scene();
```

3D 객체, 조명, 배경, 안개 등을 담는 공간입니다.

### 5.2 Camera: 카메라

```javascript
const camera = new THREE.PerspectiveCamera(
  42,
  innerWidth / innerHeight,
  0.08,
  130
);
```

PerspectiveCamera는 원근감을 표현하는 카메라입니다.

인수의 의미:

1. 시야각(FOV)
2. 화면 종횡비(가로 / 세로)
3. 가까운 렌더링 경계
4. 먼 렌더링 경계

카메라 위치는 다음과 같이 지정합니다.

```javascript
camera.position.set(x, y, z);
```

### 5.3 Renderer: 화면에 3D 장면 출력

```javascript
const renderer = new THREE.WebGLRenderer({
  antialias: true,
  preserveDrawingBuffer: true
});

renderer.setSize(innerWidth, innerHeight);
document.getElementById('stage').appendChild(renderer.domElement);
```

- `WebGLRenderer`: WebGL을 이용해 장면을 화면에 출력
- `antialias`: 계단 현상 완화
- `preserveDrawingBuffer`: 화면 캡처 등에서 렌더링 결과를 유지하는 데 사용
- `setSize`: 렌더링 화면 크기 설정
- `appendChild`: 생성된 Canvas를 HTML 컨테이너에 삽입

각 파일은 실제로 자신의 화면 크기와 성능 조건에 맞춰 Renderer 옵션을 추가 설정합니다.

### 5.4 Geometry: 3D 형태

Geometry는 3D 물체의 기본 모양입니다.

두 파일에서 사용하는 대표적인 형태:

| Geometry | 모양 |
|---|---|
| `BoxGeometry` | 직육면체 |
| `PlaneGeometry` | 평면 |
| `CylinderGeometry` | 원기둥 |
| `SphereGeometry` | 구 |
| `TorusGeometry` | 도넛형 고리 |
| `TubeGeometry` | 곡선을 따라가는 튜브 |

예시:

```javascript
const geometry = new THREE.BoxGeometry(2, 1, 3);
```

### 5.5 Material: 표면 재질

Material은 물체의 색상, 금속성, 거칠기, 투명도 등을 결정합니다.

```javascript
const material = new THREE.MeshStandardMaterial({
  color: '#c99e6f',
  roughness: 0.68,
  metalness: 0.02
});
```

주요 속성:

- `color`: 기본 색상
- `roughness`: 표면 거칠기
- `metalness`: 금속성
- `transparent`: 투명도 사용 여부
- `opacity`: 불투명도
- `emissive`: 자체 발광 색상
- `map`: 텍스처 이미지

버스 파일은 유리나 도장 표현 등에 `MeshPhysicalMaterial`도 사용합니다.

### 5.6 Mesh: 형태와 재질 결합

```javascript
const mesh = new THREE.Mesh(geometry, material);
scene.add(mesh);
```

Geometry와 Material을 결합해 실제 3D 물체를 만듭니다.

### 5.7 Group: 객체 묶기

```javascript
const group = new THREE.Group();
scene.add(group);
group.add(mesh);
```

여러 부품을 하나의 그룹으로 묶으면 위치·회전·스케일을 함께 제어할 수 있습니다.

버스 파일은 프레임, 배터리, 차체 외판, 유리, 도어, 실내 등을 그룹 단위로 관리합니다. 교실 파일도 건축 구조와 가구, 학생, 센서 등을 그룹으로 구성합니다.

### 5.8 Light: 조명

대표적인 조명 종류:

```javascript
const hemi = new THREE.HemisphereLight(0xffffff, 0x777777, 1.5);
scene.add(hemi);

const sun = new THREE.DirectionalLight(0xffffff, 2.0);
sun.position.set(-10, 13, 4);
scene.add(sun);
```

- `HemisphereLight`: 하늘과 바닥 방향의 부드러운 조명
- `DirectionalLight`: 태양광처럼 특정 방향에서 들어오는 조명
- `PointLight`: 한 지점에서 사방으로 퍼지는 조명

### 5.9 OrbitControls: 카메라 조작

```javascript
const controls = new OrbitControls(camera, renderer.domElement);

controls.enableDamping = true;
controls.dampingFactor = 0.06;
controls.enableZoom = true;
controls.enableRotate = true;
controls.enablePan = true;
```

- 마우스 드래그: 회전
- 마우스 휠: 확대 및 축소
- 우클릭 드래그: 이동(Pan)
- `enableDamping`: 부드러운 관성 효과
- `minDistance`, `maxDistance`: 확대·축소 범위 제한

### 5.10 Animation Loop: 실시간 렌더링

```javascript
function animate() {
  requestAnimationFrame(animate);

  // 애니메이션 상태 갱신

  controls.update();
  renderer.render(scene, camera);
}

animate();
```

`requestAnimationFrame()`은 브라우저의 화면 갱신 주기에 맞춰 다음 프레임을 요청합니다. 이 반복 과정에서 물체 위치, 회전, 조명, 카메라 상태 등을 갱신하고 `renderer.render()`로 화면을 다시 그립니다.

---

## 6. 스마트 학교 교실 코드의 세부 구조

### 6.1 문서와 화면 영역

교실 파일의 HTML은 크게 다음 영역으로 나뉩니다.

| 영역 | 주요 ID / 클래스 | 역할 |
|---|---|---|
| 3D 화면 | `#stage` | Three.js Canvas가 들어가는 공간 |
| 화면 음영 | `#shade` | 배경 시각 효과 |
| 상단 제목 | `.head` | 프로젝트 제목과 상태 |
| 상단 버튼 | `.top-actions` | JSON, CSV, PNG 내보내기 |
| 환경 패널 | `#ctrlPanel` | 센서와 설비 제어 |
| 카메라 버튼 | `#cameraButtons` | 카메라 시점 선택 |
| 장면 옵션 | `#tagToggle`, `#peopleToggle` | 라벨·학생 모델 표시 |
| 센서 차트 | `#history` | CO₂ 추이 Canvas |
| 로딩 화면 | `#loading` | 초기 로딩 및 오류 표시 |
| 그래픽 오류 | `#graphicsNotice` | WebGL 복구 안내 |

### 6.2 sceneSpec JSON 데이터

교실 파일에는 `id="sceneSpec"`인 `application/json` 스크립트 블록이 있습니다.

```html
<script type="application/json" id="sceneSpec">
{
  "title": "SMART CLASSROOM",
  "version": "1.1.0-camera-stable",
  "room": {
    "width": 12.8,
    "depth": 9.6,
    "height": 3.7
  }
}
</script>
```

이 블록은 실행용 JavaScript 코드가 아니라 장면의 설정을 저장한 JSON 데이터입니다.

JavaScript에서는 다음과 같이 읽습니다.

```javascript
const SPEC = JSON.parse(
  document.getElementById('sceneSpec').textContent
);
```

주요 데이터:

- `room`: 교실 크기와 벽 위치
- `style`: 재질과 색상 팔레트
- `furniture`: 책상, 칠판, 문, 창문 등 배치 정보
- `digitalTwin`: 센서 이름, 초기값, 계산식, 시나리오
- `lighting`: 조명 구성
- `cameraViews`: 카메라 위치와 시점
- `objectGroups`: 장면의 객체 그룹 목록

### 6.3 초기화 및 오류 처리

교실 파일에는 Three.js 모듈 실행 전 별도의 일반 JavaScript 스크립트가 있습니다.

주요 역할:

- `showStartupError()`: 초기화 실패 화면 표시
- `window.addEventListener('error', ...)`: 일반 실행 오류 감지
- `window.addEventListener('unhandledrejection', ...)`: 처리되지 않은 Promise 오류 감지
- `setTimeout(...)`: 일정 시간 안에 초기화가 끝나지 않으면 오류 안내
- `window.__SMART_CLASSROOM_FAIL__`: 모듈 쪽에서도 오류 표시 기능을 호출할 수 있도록 연결

WebGL 컨텍스트가 손실되거나 복구되는 상황도 별도로 감지합니다.

### 6.4 3D 객체 생성 함수

교실 코드에는 반복적인 3D 객체 생성을 편리하게 하기 위한 함수들이 있습니다.

| 함수 | 역할 |
|---|---|
| `add()` | 객체에 이름을 지정하고 부모에 추가 |
| `group()` | THREE.Group 생성 |
| `bx()` | BoxGeometry 기반 물체 생성 |
| `plane()` | PlaneGeometry 기반 평면 생성 |
| `cyl()` | CylinderGeometry 기반 원기둥 생성 |
| `sphere()` | SphereGeometry 기반 구 생성 |
| `rod()` | 두 점을 잇는 막대 형태 생성 |
| `canvasTexture()` | Canvas를 Three.js 텍스처로 변환 |
| `texCanvas()` | 그리기 함수를 이용해 Canvas 텍스처 생성 |
| `rng()` | 시드 기반 난수 생성 |

이런 함수들을 이용해 외부 3D 모델 파일을 가져오는 대신 코드로 교실의 형태와 표면을 구성합니다.

### 6.5 디지털 트윈 상태와 계산

교실은 센서와 설비 상태를 JavaScript 객체에 보관합니다. 코드에서 사용하는 주요 변수는 다음과 같습니다.

- `occupancy`: 재실 인원
- `outdoorDaylightPercent`: 외부 자연광 비율
- `temperatureTargetC`: 목표 온도
- `ventilationPercent`: 환기 출력
- `ledBrightnessPercent`: LED 밝기
- `blindsOpenPercent`: 블라인드 개방 정도
- `roomTemp`: 시뮬레이션 실내 온도
- `co2`: 시뮬레이션 CO₂ 농도

주요 함수:

| 함수 | 역할 |
|---|---|
| `calcLux()` | 자연광과 LED 설정을 이용한 조도 계산 |
| `updateVisual()` | 시뮬레이션 값에 따라 3D 장면 갱신 |
| `updateUI()` | 센서 숫자와 상태 문구 갱신 |
| `drawHistory()` | CO₂ 이력 차트 그리기 |
| `readInputs()` | 슬라이더 입력값 읽기 |
| `scenarioSelect()` | 수업·쉬는 시간·환기·야간 시나리오 적용 |
| `setView()` | 카메라 시점 변경 |
| `sample()` | 시간별 시뮬레이션 데이터 기록 |
| `registry()` | 3D 객체의 이름·종류·위치 등 목록 생성 |
| `download()` | 파일 다운로드 처리 |
| `animate()` | 시간 진행과 화면 렌더링 반복 |

교실의 계산식은 `sceneSpec.digitalTwin.calculation`에도 설명되어 있습니다. 이 값들은 교육용으로 단순화한 계산이며 정밀한 건축·공조 엔지니어링 모델이 아닙니다.

### 6.6 사용자 입력과 이벤트 연결

HTML의 슬라이더와 버튼은 JavaScript 이벤트 리스너로 연결됩니다.

예시:

```javascript
for (const id of ['occ', 'sun', 'setTemp', 'vent', 'lights', 'blinds']) {
  $(id).addEventListener('input', readInputs);
}
```

슬라이더를 움직이면 `readInputs()`가 실행되고, 내부 시뮬레이션 상태와 UI 및 3D 표현이 갱신됩니다.

---

## 7. 전기버스 스마트팩토리 코드의 세부 구조

### 7.1 화면 영역

버스 파일은 3열 레이아웃을 기본으로 구성합니다.

| 영역 | 주요 ID / 클래스 | 역할 |
|---|---|---|
| 좌측 패널 | `#sidebar` | 공정 선택 및 조작 |
| 공정 목록 | `#stage-list` | 8단계 조립 공정 |
| 3D 화면 | `#world` | Three.js Canvas |
| 상단 헤더 | `.floating-header` | 프로젝트 이름과 화면 저장 |
| 카메라 버튼 | `#view-tools` | 카메라 시점 변경 |
| 우측 버튼 | `.right-tools` | X-RAY, 360°, RESET |
| 하단 진행 표시 | `.bottom-bar` | 단계, 진행률, 속도 |
| 우측 관제 | `.inspect` | KPI, 부품 설명, 이벤트 로그 |
| 도움말 | `#help` | dialog 형태의 안내창 |
| 오류 화면 | `#fallback` | 3D 초기화 실패 시 안내 |

### 7.2 공정 데이터 배열

버스 파일은 `stageData` 배열에 8단계 공정의 제목과 설명을 저장합니다.

```javascript
const stageData = [
  {
    title: '섀시 프레임',
    sub: '강재 프레임 / 하부 플랫폼',
    desc: '차량의 기초 구조를 구성합니다.',
    detail: '교육용 개념 모델입니다.'
  }
  // 나머지 공정 데이터
];
```

실제 파일에는 다음 8단계가 정의되어 있습니다.

1. 섀시 프레임
2. 차축·바퀴
3. 배터리·전기 구동계
4. 차체 골격
5. 외판·지붕 도장
6. 창문·출입문
7. 실내·편의시설
8. 완성·품질 검사

각 단계는 `title`, `sub`, `desc`, `detail` 속성으로 화면에 표시할 정보를 관리합니다.

### 7.3 3D 모델 생성 함수

| 함수 | 역할 |
|---|---|
| `G()` | Geometry와 Material을 결합해 Mesh 생성 |
| `bx()` | 박스 형태 부품 생성 |
| `cyl()` | 원기둥 형태 부품 생성 |
| `sph()` | 구 형태 부품 생성 |
| `tube()` | 곡선을 따라가는 튜브 생성 |
| `canvasLabel()` | Canvas 기반 텍스트 텍스처 생성 |
| `labelPlane()` | 텍스트가 표시되는 평면 생성 |
| `makeRobot()` | 공장 로봇 모델 생성 |
| `part()` | 조립 부품의 정보와 상태를 등록 |

버스는 부품별로 Group을 만들고, 각 부품의 조립 위치와 분해 위치를 관리합니다.

`part()` 함수는 부품 ID, 이름, 조립 단계, 설명, 그룹, 기본 위치, 분해 위치 등의 정보를 하나의 레코드로 등록합니다. 이를 통해 공정별 표시와 분해 보기를 제어할 수 있습니다.

### 7.4 공정 제어 함수

| 함수 | 역할 |
|---|---|
| `setStage()` | 특정 조립 단계로 이동 |
| `advance()` | 이전 또는 다음 단계로 이동 |
| `autoToggle()` | 자동 공정 재생 및 정지 |
| `uiStage()` | 현재 단계에 맞춰 UI 갱신 |
| `resetHighlight()` | 부품 선택 강조 초기화 |
| `selectPart()` | 선택한 부품 정보 표시 |
| `applyXray()` | 차체 X-RAY 표시 적용 |
| `changePaint()` | 차체 색상 변경 |
| `openDoors()` | 출입문 애니메이션 |
| `setExplode()` | 분해 보기 전환 |
| `setView()` | 카메라 시점 변경 |
| `log()` | 공정 이벤트 로그 추가 |
| `resize()` | 화면 크기에 맞춰 렌더러와 카메라 조정 |
| `showFailure()` | 초기화 실패 화면 표시 |

### 7.5 부품 선택: Raycaster

버스 파일은 Three.js의 `Raycaster`를 이용해 3D 모델을 클릭했을 때 어떤 부품을 선택했는지 판별합니다.

```javascript
const raycaster = new THREE.Raycaster();
const pointer = new THREE.Vector2();
```

기본 개념:

1. 마우스 좌표를 브라우저 화면 기준으로 받습니다.
2. 화면 좌표를 정규화된 장치 좌표(NDC)로 변환합니다.
3. `raycaster.setFromCamera()`로 카메라에서 뻗는 광선을 설정합니다.
4. `intersectObjects()`로 광선과 3D 객체의 교차 여부를 확인합니다.
5. 선택된 객체의 부품 정보를 UI에 표시합니다.

따라서 사용자는 버스의 휠, 배터리, 차체, 도어, 좌석 등을 클릭해 설명을 확인할 수 있습니다.

### 7.6 공정 애니메이션과 상태

버스의 현재 공정은 상태 객체와 부품별 단계 정보를 바탕으로 제어됩니다.

- 공정 번호와 제목
- 진행률
- 완료된 공정 수
- 자동 실행 여부
- 재생 속도
- X-RAY 활성화 여부
- 분해 보기 활성화 여부
- 도어 상태
- 카메라 자동 회전 상태

자동 실행은 시간 흐름에 따라 공정 단계를 진행하며, `requestAnimationFrame()` 기반 렌더링 루프에서 3D 상태를 갱신합니다.

---

## 8. 두 프로젝트의 차이점 비교

| 구분 | 스마트 학교 교실 | 전기버스 스마트팩토리 |
|---|---|---|
| Three.js 버전 | 0.164.1 | 0.180.0 |
| 핵심 목적 | 교실 환경 제어 시뮬레이션 | 전기버스 조립 공정 체험 |
| 주요 데이터 | 온도, CO₂, 조도, 재실 인원 | 공정 단계, 부품, 조립 상태 |
| 주요 조작 | 슬라이더, 시나리오, 카메라 | 공정 버튼, 부품 클릭, X-RAY |
| 3D 객체 구성 | 교실 건축·가구·학생·설비 | 공장·로봇·버스 부품 |
| 상호작용 | 설비 값에 따른 장면 변화 | 공정 진행에 따른 부품 조립 |
| 내보내기 | JSON, CSV, PNG | PNG 화면 저장 |
| 주요 추가 기술 | 시뮬레이션 차트, 센서 라벨 | Raycaster, 분해 보기, 부품 선택 |
| 반응형 UI | 모바일 제어 패널 | 모바일 사이드바 |

두 파일 모두 HTML, CSS, JavaScript, Three.js를 사용하지만, 상태를 표현하는 방식과 사용자 상호작용의 목적은 서로 다릅니다.

---

## 9. 자주 확인해야 하는 코드 문법과 수정 위치

### 9.1 프로젝트 제목 변경

HTML의 `<title>`과 화면 제목 요소를 수정합니다.

```html
<title>프로젝트 제목</title>
```

### 9.2 화면 색상 변경

각 파일의 `<style>` 안에 있는 `:root`의 CSS 변수를 확인합니다.

교실 예시:

```css
:root {
  --deep: #101e27;
  --ink: #f5f8f7;
  --teal: #72dfcb;
}
```

버스 예시:

```css
:root {
  --bg: #08131f;
  --panel: #101d2b;
  --blue: #3c97d5;
}
```

### 9.3 Three.js 버전 변경

`importmap` 안의 CDN 주소에서 버전 번호를 변경합니다.

단, Three.js와 addons는 같은 버전으로 맞추는 것이 안전합니다. 버전 변경 후에는 모듈 API 호환성을 확인해야 합니다.

### 9.4 카메라 초기 위치 변경

```javascript
camera.position.set(x, y, z);
```

교실은 `SPEC.cameraViews`의 시점 데이터도 사용합니다. 따라서 기본 시점이나 프리셋을 바꾸려면 해당 설정과 `setView()` 구현을 함께 확인해야 합니다.

### 9.5 HTML 버튼 동작 변경

HTML 버튼의 `id`와 JavaScript의 `addEventListener()` 연결을 함께 확인합니다.

```html
<button id="next">다음</button>
```

```javascript
document.getElementById('next')
  .addEventListener('click', () => {
    // 다음 단계 실행
  });
```

ID를 HTML에서 변경했다면 JavaScript에서도 같은 ID를 수정해야 합니다.

### 9.6 반응형 화면 변경

`@media` 안의 기준 너비를 조정합니다.

```css
@media (max-width: 780px) {
  /* 모바일 화면 스타일 */
}
```

---

## 10. 실행 오류와 해결 방법

| 증상 | 확인할 내용 | 해결 방법 |
|---|---|---|
| 로딩 화면에서 멈춤 | 인터넷, CDN 연결 | 인터넷 연결 및 CDN 접근 확인 |
| `Failed to resolve module specifier` | import map 누락·오류 | `importmap`의 모듈 경로 확인 |
| `CORS` 또는 모듈 로딩 오류 | `file://` 직접 실행 | Live Server 또는 Python 서버 사용 |
| 화면이 어둡거나 3D가 안 보임 | WebGL·그래픽 가속 | Chrome/Edge 그래픽 가속 및 WebGL 확인 |
| 조작 버튼이 반응하지 않음 | HTML ID와 JS ID 불일치 | `id`와 `getElementById()` 확인 |
| 모바일에서 패널이 겹침 | 반응형 CSS | `@media`의 위치·크기·z-index 확인 |
| 프레임이 끊김 | GPU·그림자·메시 수 | 픽셀 비율, 그림자, 조명, 객체 수 조정 |
| 카메라가 이상한 위치로 이동 | 카메라 프리셋·OrbitControls | 카메라 위치와 target 확인 |

### 교실 파일의 오류 처리 특징

교실 파일은 초기화 오류, 처리되지 않은 Promise 오류, WebGL 컨텍스트 손실과 복구 이벤트를 감지하는 코드가 포함되어 있습니다.

### 버스 파일의 오류 처리 특징

버스 파일은 Renderer 생성 과정의 예외 처리와 `showFailure()`를 통해 로딩 실패 시 대체 안내 화면을 보여 주는 구조를 포함합니다. 초기 로딩이 일정 시간 이상 지연될 때도 대체 화면을 표시하도록 구성되어 있습니다.

---

## 11. 코드 수정 시 주의사항

1. HTML의 `id`를 수정할 때 JavaScript에서 참조하는 ID도 함께 변경합니다.
2. `importmap`의 Three.js와 addons 버전은 서로 일치시킵니다.
3. `<script type="module">`을 일반 `<script>`로 바꾸지 않습니다.
4. 3D 객체를 생성한 뒤에는 적절한 Group 또는 Scene에 추가해야 화면에 표시됩니다.
5. 카메라 위치만 바꾸는 것이 아니라 `controls.target`도 함께 확인해야 합니다.
6. 애니메이션 루프를 중복 실행하지 않도록 주의합니다.
7. `requestAnimationFrame()` 안에서 불필요하게 Geometry나 Material을 계속 생성하지 않도록 합니다.
8. 시뮬레이션 값은 실제 센서 측정값으로 오해되지 않도록 표시합니다.
9. 공정 진행률이나 품질 상태는 코드상 가상 상태이며 실제 제조 품질 검사 결과가 아닙니다.
10. 파일을 수정한 뒤에는 두 프로젝트를 각각 다시 실행해 버튼, 카메라, 화면 크기, 콘솔 오류를 확인합니다.

---

## 12. 전체 구조 요약

두 프로젝트는 다음과 같은 계층으로 이해하면 됩니다.

```text
웹 브라우저
│
├── HTML
│   ├── 화면 컨테이너
│   ├── 버튼과 입력 요소
│   ├── 상태 표시 패널
│   └── Canvas 영역
│
├── CSS
│   ├── 색상과 디자인
│   ├── 레이아웃
│   └── 반응형 화면
│
└── JavaScript ES Module
    ├── Three.js 라이브러리
    ├── Scene / Camera / Renderer
    ├── Geometry / Material / Mesh
    ├── Group / Light
    ├── OrbitControls
    ├── 프로젝트별 상태 데이터
    ├── 사용자 이벤트 처리
    ├── 3D 장면 갱신
    └── Animation Loop
```

**핵심적으로 기억할 부분**

- HTML은 화면의 구조를 만듭니다.
- CSS는 화면의 디자인과 배치를 담당합니다.
- JavaScript는 버튼, 입력, 데이터, 애니메이션을 제어합니다.
- Three.js는 3D 공간과 물체를 생성하고 화면에 렌더링합니다.
- OrbitControls는 사용자가 3D 카메라를 직접 조작하도록 합니다.
- `requestAnimationFrame()`은 장면을 지속적으로 갱신합니다.

이 구조를 이해하면 두 파일에서 UI를 수정할 부분, 3D 모델을 수정할 부분, 시뮬레이션 로직을 수정할 부분을 구분해 작업할 수 있습니다.
