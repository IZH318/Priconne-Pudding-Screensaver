# Priconne-Pudding-Screensaver
[![Live Demo](https://img.shields.io/badge/Live%20Demo-Visit-brightgreen)](https://izh318.github.io/Priconne-Pudding-Screensaver/)<br>
이 문서는 영어로도 제공됩니다. / This document is also available in English. ➡️ [**English Version**](README.en.md)
---

![_2025_06_30_03_01_36_712-ezgif com-optimize](https://github.com/user-attachments/assets/28f20819-704c-41a8-89b4-0b88fe322686)<br>
*(▲ 실제 작동 예시 GIF)*

웹 브라우저에서 실행되는 간단한 화면보호기 프로젝트입니다.<br>
DVD 화면보호기처럼, 푸딩으로 만들어진 프린세스 커넥트! Re:Dive의 다양한 캐릭터 이미지가 화면 가장자리에 닿을 때마다 튕겨 나옵니다.

## ✨ 주요 기능
* **클래식 바운싱 애니메이션**: 이미지가 화면 끝에 닿으면 튕겨 나옵니다.
* **랜덤 이미지 변경**: 벽에 부딪힐 때마다 다양한 푸딩 캐릭터의 모습으로 이미지가 랜덤으로 변경됩니다.
* **스마트 충돌 감지**: 이미지의 사각형 영역이 아닌, 투명한 부분을 제외한 실제 이미지 영역을 기준으로 충돌을 감지하여 훨씬 자연스러운 움직임을 보여줍니다.
* **동적 이미지 로딩**: `img` 폴더에 있는 `psy_pudding_still_100.png` 부터 `psy_pudding_still_165.png` 까지의 이미지들을 자동으로 불러와 애니메이션에 사용합니다.
* **완벽한 반응형 및 모바일 최적화**: 브라우저 창 크기가 변경되어도 애니메이션이 자연스럽게 유지되며, 모바일 환경의 주소창 변화에도 대응하도록 최적화되었습니다.

## 🚀 사용 방법
### 1. 온라인에서 바로 확인하기
아래 링크를 클릭하여 웹 브라우저에서 바로 스크린세이버를 실행할 수 있습니다. (* 별도의 설치가 필요 없습니다.)<br>
**[➡️ Live Demo 바로가기](https://izh318.github.io/Priconne-Pudding-Screensaver/)**

### 2. 로컬에서 실행 및 수정하기
코드를 직접 수정하거나 자신만의 이미지를 추가하고 싶다면, 아래 방법을 따르세요.

```
├── img/
│   ├── psy_pudding_still_100.png
│   ├── psy_pudding_still_101.png
│   ├── ...
│   ├── psy_pudding_still_164.png
│   └── psy_pudding_still_165.png
├── index.html
├── script.js
└── style.css
```

1.  이 리포지토리를 다운로드하거나 복제(clone)합니다.
2.  `index.html` 파일을 웹 브라우저에서 열면 바로 실행됩니다.

## 🎨 커스터마이징 (Customization)
#### 나만의 이미지 추가하기
규칙적인 파일명을 따르지 않는 자신만의 이미지를 화면보호기에 추가할 수 있습니다.

1.  사용하고 싶은 이미지 파일을 프로젝트 폴더 내 원하는 위치에 추가합니다. (예: `img/my_image.png`)
2.  `script.js` 파일을 열어 `manualFiles` 배열을 찾습니다.
3.  배열 안에 이미지 파일의 경로를 다음과 같이 문자열로 추가합니다.

```javascript
// 1. 수동으로 추가할 이미지 목록
const manualFiles = [
  // 여기에 규칙 없는 파일 추가. 예: 'img/special.gif'
  'img/my_custom_pudding.png',
  'img/another_image.gif'
];
```
이렇게 추가된 이미지는 기존 푸딩 이미지들과 함께 화면보호기에 나타납니다.

## 🔧 구조 및 구현
이 프로젝트는 순수 JavaScript, HTML, CSS로만 제작되었습니다.

* **`index.html`**: 화면보호기가 표시될 기본 `<div>`와 이미지를 담을 `<img>` 태그를 포함하는 기본 구조입니다.
* **`style.css`**: 스크롤바를 숨기고, 검은 배경의 전체 화면 레이아웃을 만듭니다. `will-change: transform;` 속성을 사용하여 애니메이션 성능을 최적화하고, `var(--app-height)` CSS 변수를 이용해 **모바일 뷰포트 높이에 동적으로 대응**합니다.
* **`script.js`**: 이 프로젝트의 핵심 로직을 담당합니다.
    * `setRealViewportHeight()`: 모바일 브라우저에서 주소창이 사라지거나 나타날 때 변하는 실제 뷰포트 높이(`window.innerHeight`)를 계산하여 CSS 변수 `--app-height`에 적용합니다.
    * `initializeScreenSaver()`: 페이지가 로드될 때, 지정된 폴더의 모든 이미지를 비동기적으로 불러오고 각 이미지의 실제 콘텐츠 영역(투명 픽셀 제외)을 분석합니다. 또한, 최초 실행 시 화면 높이를 설정하고 **초기 이미지를 콘솔에 기록**합니다.
    * `analyzeImageBounds()`: `canvas` API를 사용하여 이미지의 모든 픽셀을 스캔하고, 알파(alpha) 값이 0보다 큰 픽셀들의 경계를 계산합니다. 이 정보는 '스마트 충돌 감지'에 사용됩니다.
    * `animate()`: `requestAnimationFrame`을 사용하여 부드러운 애니메이션 루프를 실행합니다. 이 함수 안에서 이미지의 좌표를 업데이트하고, `analyzeImageBounds`에서 얻은 데이터를 기반으로 충돌을 감지하며, 충돌 발생 시 **지연 없이 즉시** `changeImage()` 함수를 호출합니다.
    * `changeImage()`: 벽 충돌 시 호출됩니다. 현재 이미지를 제외한 다른 이미지 중에서 **무작위로 하나를 선택**하여 즉시 변경합니다. 변경된 이미지 경로는 개발자 콘솔에 출력됩니다.

## 📜 저작권 및 출처 (Attribution)
이 프로젝트에 사용된 모든 캐릭터 이미지의 저작권은 **Cygames, Inc.** 에 있습니다.

이미지들은 **프린세스 커넥트! Re:Dive 클라이언트**에서 추출된 리소스를 기반으로 합니다.<br>
(* 이 프로젝트는 팬 활동의 일환으로 제작되었으며, 상업적 목적이 없습니다.)

## 📄 라이선스
이 프로젝트의 코드는 [MIT License](LICENSE)에 따라 배포됩니다. 이미지 저작권은 원 저작권자인 Cygames, Inc.를 따릅니다.
