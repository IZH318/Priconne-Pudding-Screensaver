# Priconne-Pudding-Screensaver

![_2025_06_29_05_07_15_298-ezgif com-optimize](https://github.com/user-attachments/assets/ada858d5-4c10-49c7-9f9f-272feb30f8c5)<br>
*(▲ GIF example of the screensaver in action)*

This is a simple screensaver project that runs in a web browser.<br>
Like the classic DVD screensaver, various character images from Princess Connect! Re:Dive, styled as pudding, bounce off the edges of the screen.

## ✨ Key Features
*   **Classic Bouncing Animation**: The image bounces off when it hits the edge of the screen.
*   **Image Change on Collision**: The image changes to a different pudding character each time it hits a wall.
*   **Smart Collision Detection**: Collision is detected based on the **actual image area, excluding transparent parts**, rather than the rectangular bounding box, resulting in much more natural movement.
*   **Dynamic Image Loading**: Automatically loads and uses images from `psy_pudding_still_100.png` to `psy_pudding_still_165.png` located in the `img` folder for the animation.
*   **Responsive Design**: The animation adapts smoothly even when the browser window is resized.

## 📂 File Structure and Setup
The project's file structure is as follows. All image files are included, so no separate downloads are necessary.

```
├── img/
│   ├── psy_pudding_still_100.png
│   ├── psy_pudding_still_101.png
│   └── ...
│   ├── psy_pudding_still_164.png
│   └── psy_pudding_still_165.png
├── index.html
├── script.js
└── style.css
```

1.  Download this repository (or the files from the Release).
2.  Open the `index.html` file in a web browser to run it immediately.

## 🎨 Customization

#### Adding Your Own Images
You can add your own images to the screensaver, even if they don't follow the regular file naming convention.

1.  Add the image file you want to use to your desired location within the project folder (e.g., `img/my_image.png`).
2.  Open the `script.js` file and find the `manualFiles` array.
3.  Add the path to your image file as a string to the array, like so:

```javascript
// 1. List of manually added images
const manualFiles = [
  // Add files with irregular names here. e.g., 'img/special.gif'
  'img/my_custom_pudding.png',
  'img/another_image.gif'
];
```
Images added this way will appear in the screensaver alongside the default pudding images.

## 🔧 Technical Details

This project was built using only pure JavaScript, HTML, and CSS.

*   **`index.html`**: The basic structure containing the `<div>` where the screensaver is displayed and the `<img>` tag for the image.
*   **`style.css`**: Creates a full-screen layout with a black background, hides the scrollbar, and uses the `will-change: transform;` property to optimize animation performance.
*   **`script.js`**: Handles the core logic of the project.
    *   `initializeScreenSaver()`: When the page loads, it asynchronously loads all images from the specified folder and analyzes the actual content area (excluding transparent pixels) of each image.
    *   `analyzeImageBounds()`: Uses the `canvas` API to scan every pixel of an image and calculates the boundaries of pixels with an alpha value greater than 0. This information is used for 'Smart Collision Detection'.
    *   `animate()`: Runs a smooth animation loop using `requestAnimationFrame`. Inside this function, it updates the image's coordinates and detects collisions based on the data obtained from `analyzeImageBounds`.
    *   `changeImageWithCooldown()`: Changes the image upon wall collision and implements a short cooldown (250ms) to prevent the image from changing too rapidly in corners.

## 📜 Attribution

The copyright for all character images used in this project belongs to **Cygames, Inc.**

The images are based on resources extracted from the **Princess Connect! Re: Dive client**.<br>
(* This project was created as a fan work and has no commercial purpose.)

## 📄 License

The code for this project is distributed under the [MIT License](LICENSE). The image copyrights follow those of the original copyright holder, Cygames, Inc.
