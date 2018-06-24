<template>
<div class='display'>
  <Digit :digit='digits[0]'></Digit>
  <Digit :digit='digits[1]'></Digit>
  <div class='colon'>
    <div class='dot'>&nbsp;</div>
    <div class='dot'>&nbsp;</div>
  </div>
  <Digit :digit='digits[2]'></Digit>
  <Digit :digit='digits[3]'></Digit>
  <div class='colon'>
    <div class='dot'>&nbsp;</div>
    <div class='dot'>&nbsp;</div>
  </div>
  <Digit :digit='digits[4]'></Digit>
  <Digit :digit='digits[5]'></Digit>
</div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import Digit from './Digit.vue';

function getDigit(num: number, dig: number): number {
  return Math.floor(num / (10 ** dig)) % 10;
}

@Component({
  components: {
    Digit
  },
})
export default class Display extends Vue {
  @Prop() private date!: Date;
  get hours () {
    return this.date.getHours()
  }
  get minutes () {
    return this.date.getMinutes()
  }
  get seconds () {
    return this.date.getSeconds()
  }
  get digits () {
    return [
      getDigit(this.hours, 1),
      getDigit(this.hours, 0),
      getDigit(this.minutes, 1),
      getDigit(this.minutes, 0),
      getDigit(this.seconds, 1),
      getDigit(this.seconds, 0),
    ]
  }
}
</script>

<style scoped>
.display {
  display: grid;
  grid-template-columns: repeat(2, 1fr) 0.25fr repeat(2, 1fr) 0.25fr repeat(2, 1fr);
}
.colon {
  margin: 60% 0px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}
.dot {
  background-color: red;
  width: 80%;
  border-radius: 20%;
}
</style>
