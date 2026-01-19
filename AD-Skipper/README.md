# AD-Skipper
A small code to skip Ads on YT.

# How To?
1. Open Chrome.
2. Then open YouTube or other video streaming platform.
3. Open `Developer Tools` by shortcut `CTRL + SHIFT + I`.
4. Open Console Tab.
5. Clear by shortcut `CTRL + L`.
6. Copy and Paste the code below in it :
```
setInterval(() => {
  const skipButton = document.querySelector('.ytp-ad-skip-button.ytp-button');
  if (skipButton) {
    skipButton.click();
    console.log('Skipped ad');
  }
  const adOverlay = document.querySelector('.ad-showing');
  const video = document.querySelector('video');
  if (adOverlay && video) {
    video.muted = true;
    video.currentTime = video.duration;
    console.log('Fast-forwarded unskippable ad');
  }
}, 500);
```
7. Press Enter.
8. Close the developer tools.
9. Now, when switch to new tab or open new tab then the video is paused and when returned to youtube video it plays automatically.