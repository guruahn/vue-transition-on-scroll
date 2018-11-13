# Transition On Scroll

> It is Vue.js plugin. When you scroll, you can give the transition effect to the internal objects.
when the target object show up in viewport of wrapper(or window), transition effect start.

## Install
```
npm install vue-transition-on-scroll
yarn add vue-transition-on-scroll
```

## Example

```html
<template>
  <div class="section scroll-transition">
    <div class="inner">
      <div>
        scroll down
      </div>
      <div id="scroll1">
        <trans-on-scroll wrapper=".scroll-transition" repeat>from default(top)</trans-on-scroll>
      </div>
      <div id="scroll2">
        <trans-on-scroll wrapper=".scroll-transition" repeat from="right">from right</trans-on-scroll>
      </div>
      <div id="scroll3">
        <trans-on-scroll wrapper=".scroll-transition" repeat from="left">from left</trans-on-scroll>
      </div>
    </div>
  </div>
</template>
```

```scss
.scroll-transition {
  height: 300px;
  overflow: scroll;
  font-size: 3em;
  &::-webkit-scrollbar {
    width: 8px;
  }
  &::-webkit-scrollbar-thumb {
    background-color: rgba(31, 45, 61, 0.14);
    outline: 1px solid rgba(31, 45, 61, 0.14);
    border-radius: 4px;
  }
  .inner {
    height: 1500px;
    &>div {
      height: 300px;
      margin-bottom: 20px;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }
  }
  #scroll1 {
    background-color: #50C3F7;
  }
  #scroll2 {
    background-color: #7986CB;
  }
  #scroll3 {
    background-color: #AED581;
  }
}
```

## Props

| Property  | Description               | Type     | Accepted Values       | Default |
|-----------|---------------------------|----------|-----------------------|---------|
| from      | transition direction from | String   | top/right/left/bottom | top     |
| wrapper   | wrapper is scrollable box what box wrapped targets | String | only id | window     |
| distance  | distance of trasition     | String | long/normal/short | normal     |
| repeat    | whether repeat transiton effect | Boolean | - | false     |
