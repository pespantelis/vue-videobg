# Video Background

## Install via NPM

Available through npm as `vue-videobg`.
```
npm install --save vue-videobg
```

## Usage

```js
import VideoBg from 'vue-videobg'

Vue.component('video-bg', VideoBg)

// or
new Vue({
  el: 'body',
  components: { VideoBg }
})
```

```html
<video-bg :sources="['demo/assets/video.mp4']" img="demo/assets/bg.jpg">
  <!-- If you want to add content here, a slot is waiting! -->
</video-bg>
```

## License
VideoBackground is released under the MIT License. See the bundled LICENSE file for details.
