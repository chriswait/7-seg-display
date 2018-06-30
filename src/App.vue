<template>
  <div id="app">
    <div id='scene'>
      <div id='clock'>
        <div class='face' id='front'><Display :date="date"></Display></div>
        <div class='face' id='back'></div>
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
  margin: 0px;
}
#app {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  --clock-width: 300px;
  --clock-height: 100px;
  --clock-depth: 300px;
}
#scene {
  width: var(--clock-width);
  height: var(--clock-height);
  perspective: 1000px;
}
#clock {
  width: 100%;
  height: 100%;
  position: relative;
  transform-style: preserve-3d;
  transform: rotateX(-8deg) rotateY(-15deg);
  display: flex;
  align-items: center;
  justify-content: center;
}
.face {
  position: absolute;
  background-color: #272f2f;
  border: 1px solid black;
  transform-style: preserve-3d;
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
#front {  transform: rotateX(0deg)    rotateY(0deg)     translateZ(calc(var(--clock-depth) / 2)); }
#back {   transform: rotateX(0deg)    rotateY(180deg)   translateZ(calc(var(--clock-depth) / 2)); }
#right {  transform: rotateX(0deg)    rotateY(90deg)    translateZ(calc(var(--clock-width) / 2)); }
#left {   transform: rotateX(0deg)    rotateY(-90deg)   translateZ(calc(var(--clock-width) / 2)); }
#top {    transform: rotateX(90deg)   rotateY(0deg)     translateZ(calc(var(--clock-height) / 2)); }
#bottom { transform: rotateX(-90deg)  rotateY(0deg)     translateZ(calc(var(--clock-height) / 2)); }

#front {
}
</style>
