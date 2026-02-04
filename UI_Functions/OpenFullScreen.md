# Fullscreen Div using JavaScript

This documentation explains how to make a specific `div` element go fullscreen using a button, and how to exit fullscreen mode using JavaScript.

---

## 📌 Features

- Fullscreen only a specific `div`
- Exit fullscreen with a button
- Works in modern browsers (Chrome, Edge, Firefox, Safari)
- Uses the Fullscreen API

---

## 🧱 HTML Structure

```html
<div id="myDiv" class="box">
  <h2>This is my div</h2>
  <p>It will go fullscreen when you click the button.</p>

  <button onclick="closeFullScreen()">Exit Full Screen</button>
</div>

<button onclick="openFullScreen()">View Full Screen</button>
```

#### CSS
```css
.box {
  width: 300px;
  height: 200px;
  background: #f2f2f2;
  padding: 20px;
  border-radius: 8px;
}
```
 ```js
 const elem = document.getElementById("myDiv");

  function openFullScreen() {
    if (elem.requestFullscreen) {
      elem.requestFullscreen();
    } else if (elem.webkitRequestFullscreen) { // Safari
      elem.webkitRequestFullscreen();
    } else if (elem.msRequestFullscreen) { // IE11
      elem.msRequestFullscreen();
    }
  }

  function closeFullScreen() {
    if (document.exitFullscreen) {
      document.exitFullscreen();
    } else if (document.webkitExitFullscreen) { // Safari
      document.webkitExitFullscreen();
    } else if (document.msExitFullscreen) { // IE11
      document.msExitFullscreen();
    }
  }
  ```

***🧠 How It Works***

requestFullscreen() makes the selected div fullscreen.

exitFullscreen() exits fullscreen mode.

Vendor prefixes ensure compatibility with older browsers.

Fullscreen actions must be triggered by user interaction (e.g., button click).

***⚠️ Browser Notes***

ESC key can also exit fullscreen (browser behavior).

Fullscreen API will not work automatically on page load.

***✅ Supported Browsers***

Chrome

Edge

Firefox

Safari