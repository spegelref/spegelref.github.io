---
layout:   front
title:    Martin Lind
subtitle: Developer, nerd & creator of random things
---
<script>
const throttle = (func, limit) => {
  let lastFunc
  let lastRan
  return function() {
    const context = this
    const args = arguments
    if (!lastRan) {
      func.apply(context, args)
      lastRan = Date.now()
    } else {
      clearTimeout(lastFunc)
      lastFunc = setTimeout(function() {
        if ((Date.now() - lastRan) >= limit) {
          func.apply(context, args)
          lastRan = Date.now()
        }
      }, limit - (Date.now() - lastRan))
    }
  }
}
const eventHandler = throttle((event) => {
  const p = event.pageX / window.innerWidth;
  let fs = event.pageY / window.innerHeight;
  if (fs == 0) fs = 1;
  const v = Math.round(p * 100);
  const image = document.querySelector(".image");
  image.style.transform = `rotate(${p * 360}deg)`;
  document.body.style.fontSize = `${1+fs}em`;
  document.body.style.filter = `contrast(${fs * 10})`;
  document.body.style.transform = `rotate3d(${p}, ${fs}, ${p/fs}, ${Math.sqrt(fs * p) * 25}deg)`;
}, 40);
window.addEventListener('mousemove', eventHandler);
</script>

This is my index page. One of the random things I do for example is this site. For now it is quite empty, I am "working" on it. Some day it may—or may not—flourish with content. For now enjoy my beautiful banner. Which is using CSS grid layout and a GitHub template image instead of my face.

## Links

I have a GitHub profile: [spegelref](https://www.github.com/spegelref)<br>
I am inactive on stack overflow: [martin-lind](https://stackoverflow.com/users/2086892/martin-lind)

## 余計–Superfluous

I have successfully added links. I don't use social networks for the kind of topics you would see here. With that typed; you can find me on some but most likely not.

With a normal screen DPI—ThinkPad T420s screen in this case—these paragraphs have the same width an A5 paper would have, with very thin margins. Yes, yes I am just filling in text to see how my index or front page on this jekyll site will render.

Last thing to add to this site is navigation, which without would prevent navigation to my posts and other content. Maybe they would fit above my header, but that would remove some "focus" from it. Placing the navigation below the header would remove the connection between it and the content. I could add the links right here, in this text; I am [writing](/posts), both guides and possibly rants.
