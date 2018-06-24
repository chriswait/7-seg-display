<template>
  <div class='digit'>
    <div
    v-for='segment in segments'
    :key='segment'
    :class="[
    'segment',
    'segment-'+segment,
    {active: activeSegments.includes(segment)},
    ]"
    >&nbsp;</div>
  </div>
</template>

<script lang='ts'>
import { Component, Prop, Vue } from 'vue-property-decorator';

let states: Array<Array<number>> = [
  [0, 1, 2, 3, 4, 5],
  [1, 2],
  [0, 1, 3, 4, 6],
  [0, 1, 2, 3, 6],
  [1, 2, 5, 6],
  [0, 2, 3, 5, 6],
  [0, 2, 3, 4, 5, 6],
  [0, 1, 2],
  [0, 1, 2, 3, 4, 5, 6],
  [0, 1, 2, 3, 5, 6]
];

@Component
export default class Digit extends Vue {
  @Prop() private digit!: number;
  private segments: Array<number> = [...Array(7).keys()];
  get activeSegments() {
    return states[this.digit];
  }
}
</script>

<style scoped>
.digit {
  margin: 8%;
  position: relative;
  --block-vertical: calc(100% / 7);
  --block-horizontal: calc(100% / 4);
}
.segment {
  background-color: rgba(50, 0, 0, 0.1);
  /* border-radius: 100%; */
  display: block;
  position: absolute;
  transition: background-color linear 0.1s;
}
.segment.active {
  background-color: red;
}
/* Horizontal */
.segment-0, .segment-3, .segment-6 {
  width: 100%;
  height: var(--block-vertical);
  clip-path: polygon(15% 50%, 27.5% 0, 72.5% 0, 85% 50%, 72.5% 100%, 27.5% 100%);
}
/* Vertical */
.segment-1, .segment-2, .segment-4, .segment-5, .segment-7 {
  width: var(--block-horizontal);
  height: calc(4 * 100% / 7);
  clip-path: polygon(100% 27%, 100% 72%, 50% 85%, 0 72%, 0 27%, 55% 15%);
}
/* Top */
.segment-0, .segment-1, .segment-5 { top: 0%; }
/* Middle */
.segment-6 { top: calc(var(--block-vertical) * 3); }
/* Bottom */
.segment-2, .segment-3, .segment-4 { bottom: 0%; }
/* Left */
.segment-0, .segment-3, .segment-4, .segment-5, .segment-6  { left: 0%; }
/* Right */
.segment-0, .segment-1, .segment-2, .segment-3              { right: 0%; }
</style>
