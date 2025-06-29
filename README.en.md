# Priconne-Pudding-Screensaver
[![Live Demo](https://img.shields.io/badge/Live%20Demo-Visit-brightgreen)](https://izh318.github.io/Priconne-Pudding-Screensaver/)<br>
This document is also available in Korean. / 이 문서는 한국어로도 제공됩니다. ➡️ [**한국어 버전**](README.md)
---

![_2025_06_30_03_01_36_712-ezgif com-optimize](https://github.com/user-attachments/assets/28f20819-704c-41a8-89b4-0b88fe322686)<br>
*(▲ Live Demo GIF)*

A simple screensaver project that runs in your web browser.<br>
Like the classic DVD screensaver, various pudding-themed characters from Princess Connect! Re:Dive bounce around the screen, changing every time they hit the edge.

## ✨ Features
* **Classic Bouncing Animation**: The image bounces off the edges of the screen.
* **Random Image Change**: The image changes to a different random pudding character upon every collision.
* **Smart Collision Detection**: Detects collisions based on the actual image content (excluding transparent areas) for much more natural movement.
* **Dynamic Image Loading**: Automatically loads images from `psy_pudding_still_100.png` to `psy_pudding_still_165.png` in the `img` folder for the animation.
* **Fully Responsive & Mobile-Optimized**: The animation remains seamless even when the browser window is resized, and it's optimized to handle the dynamic address bar in mobile browsers.

## 🚀 How to Use
### 1. View Online
Click the link below to run the screensaver directly in your web browser. (* No installation required.)<br>
**[➡️ Go to Live Demo](https://izh318.github.io/Priconne-Pudding-Screensaver/)**

### 2. Run and Modify Locally
Follow these steps if you want to modify the code or add your own images.

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

1.  Download or clone this repository.
2.  Open the `index.html` file in your web browser.

## 🎨 Customization
#### Add Your Own Images
You can add your own images to the screensaver by modifying the code in your local environment.

1.  Add your desired image files to a location within the project folder (e.g., `img/my_image.png`).
2.  Open the `script.js` file and find the `manualFiles` array.
3.  Add the path to your image file as a string within the array, like so:

```javascript
// 1. List of images to add manually
const manualFiles = [
  // Add non-sequential files here, e.g., 'img/special.gif'
  'img/my_custom_pudding.png',
  'img/another_image.gif'
];
```
Images added this way will appear in the screensaver along with the existing pudding characters.

## 🛠️ How It Works
This project is built with pure JavaScript, HTML, and CSS.

* **`index.html`**: Provides the basic structure, including a main `<div>` for the screensaver and an `<img>` tag for the image.
* **`style.css`**: Hides scrollbars and creates a full-screen layout with a black background. It uses the `will-change: transform;` property to optimize animation performance and the `var(--app-height)` CSS variable to **dynamically adapt to mobile viewport height**.
* **`script.js`**: Handles the core logic of the project.
    * `setRealViewportHeight()`: Calculates the actual viewport height (`window.innerHeight`), which changes when the mobile browser's address bar appears or disappears, and applies it to the `--app-height` CSS variable.
    * `initializeScreenSaver()`: When the page loads, it asynchronously loads all images from the specified folder and analyzes the actual content area (excluding transparent pixels) of each. It also sets the initial screen height and **logs the initial image to the console**.
    * `analyzeImageBounds()`: Uses the Canvas API to scan every pixel of an image and calculate the bounds of pixels with an alpha value greater than 0. This data is used for "Smart Collision Detection."
    * `animate()`: Runs a smooth animation loop using `requestAnimationFrame`. Inside this function, it updates the image's coordinates and detects collisions based on the data from `analyzeImageBounds`, calling `changeImage()` **immediately and without delay** upon collision.
    * `changeImage()`: Called on a wall collision. It **selects a new random image**, ensuring it's different from the current one, and applies it instantly. The path of the new image is logged to the developer console.

## 📜 Attribution
Copyright for all character images used in this project belongs to **Cygames, Inc.**

The images are based on resources extracted from the **Princess Connect! Re:Dive** client.<br>
(* This is a fan-made project and is not intended for commercial use.)

## 📄 License
The code in this project is distributed under the [MIT License](LICENSE). Image copyrights follow those of the original copyright holder, Cygames, Inc.
