<template>
  <div id="app">
    <div id='scene'>
      <div id='bg'></div>
      <div id='clock'>
        <div class='face' id='front'><Display :date="date"></Display></div>
        <div class='face' id='back'><Display :date="date"></Display></div>
        <div class='face' id='right'></div>
        <div class='face' id='left'></div>
        <div class='face' id='top'></div>
        <div class='face' id='bottom'></div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Display from './components/Display.vue';

@Component({
  components: {
    Display,
  }
})
export default class App extends Vue {
  private date: Date = new Date();
  created() {
    setInterval(() => {
      this.date = new Date();
    }, 1000);
  }
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  max-height: 100%;
  height: 100%;
  overflow: hidden;
  background-color: black;
}
#app {
  width: 100%;
  height: 100%;
}

#app {
  --clock-width: 250px;
  --clock-height: 50px;
  --clock-depth: 150px;
}
@media (min-width: 480px) and (max-width: 768px) {
  #app {
    --clock-width: 400px;
    --clock-height: 80px;
    --clock-depth: 240px;
  }
}
@media (min-width: 768px) and (max-width: 1024px) {
  #app {
    --clock-width: 450px;
    --clock-height: 90px;
    --clock-depth: 280px;
  }
}
@media (min-width: 1024px) {
  #app {
    --clock-width: 550px;
    --clock-height: 110px;
    --clock-depth: 330px;
  }
}

#scene {
  width: 100%;
  height: 100%;
  perspective: calc(var(--clock-width) * 3);
  position: relative;
}
#bg {
  height: 100%;
  width: 100%;
  position: absolute;
  background: radial-gradient(#232323, black);
}
#clock {
  height: var(--clock-height);
  width: var(--clock-width);
  top: calc(50% - var(--clock-height) / 2);
  left: calc(50% - var(--clock-width) / 2);
  position: relative;
  transform-style: preserve-3d;
  display: flex;
  align-items: center;
  justify-content: center;
  animation: rotation 10s infinite ease-in-out;
}
.face {
  position: absolute;
  background-color: rgba(39, 47, 47, 0.9);
  border: 3px solid red;
  border-radius: 3px;
}
#front, #back {
  width: var(--clock-width);
  height: var(--clock-height);
}
#left, #right {
  width: var(--clock-depth);
  height: var(--clock-height);
}
#top, #bottom {
  width: var(--clock-width);
  height: var(--clock-depth);
}
#front {  transform: rotateY(0deg)    translateZ(calc(var(--clock-depth) / 2)); }
#back {   transform: rotateY(180deg)  translateZ(calc(var(--clock-depth) / 2)); }
#right {  transform: rotateY(90deg)   translateZ(calc(var(--clock-width) / 2)); }
#left {   transform: rotateY(-90deg)  translateZ(calc(var(--clock-width) / 2)); }
#top {    transform: rotateX(90deg)   translateZ(calc(var(--clock-height) / 2)); }
#bottom { transform: rotateX(-90deg)  translateZ(calc(var(--clock-height) / 2)); }

#back > * {
  transform: rotateX(180deg) rotateY(180deg);
}

@keyframes rotation {
  from {
    transform: rotateY(0deg) rotateZ(0deg);
  }
  to {
    transform: rotateY(180deg) rotateZ(180deg);
  }
}
</style>
