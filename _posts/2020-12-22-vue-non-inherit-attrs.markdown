---
layout: post
title:  "vue 禁用 Attribute 继承"
date:   2020-12-22
categories: vue
---

### Vue 禁用 Attribute 继承

组件的 inheritAttrs 属性，指定了组件根元素是否接收来自父元素设置的 Attributes

```
Vue.component('my-component', {
  inheritAttrs: false,
  // ...
})
```

eg:

<iframe src="https://codesandbox.io/embed/inheritattrs-mq9rs?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="inheritAttrs"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>
