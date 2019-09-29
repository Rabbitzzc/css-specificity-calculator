<template>
  <div id="app">
    <specificity></specificity>
  </div>
</template>

<script>

import Specificity from './components/Specificity.vue';

export default {
  name: 'app',
  components: {
    Specificity,
  },
};
</script>

<style>
body {
  background: #229ffd;
}

* {
  list-style: none;
  margin: 0;
  padding: 0;
  outline: none;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}
html,
body {
  -webkit-tap-highlight-color: transparent;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
html {
  font-size: 16px;
}
@media (max-width: 479px) {
  html {
    font-size: 14px;
  }
}
body {
  font-family: "Noto Sans", sans-serif;
  font-weight: 400;
  line-height: 1.5;
  word-wrap: break-word;
  word-break: break-word;
  width: 100vw;
}
ul,
li {
  margin: 0;
  padding: 0;
  list-style: none;
}

img {
  max-width: 100%;
}
input,
textarea {
  -webkit-appearance: none;
  -webkit-tap-highlight-color: transparent;
}
html {
  overflow-y: scroll;
}
:root {
  overflow-y: auto;
  overflow-x: hidden;
}
:root body {
  position: absolute;
}
::-webkit-scrollbar {
  width: 0.35rem;
  height: 0.35rem;
  background: rgba(255, 255, 255, 0.6);
}
::-webkit-scrollbar-track {
  border-radius: 0;
}
::-webkit-scrollbar-thumb {
  border-radius: 0;
  background-color: rgba(100, 100, 100, 0.4);
  transition: all 0.2s;
}
::-webkit-scrollbar-thumb:hover {
  background-color: rgba(100, 100, 100, 0.7);
}

</style>
