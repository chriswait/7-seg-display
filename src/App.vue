<template>
  <div id="app">
    <Display class='display1' :date="date"></Display>
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
.display1 {
  width: 600px;
  max-width: 100%;
  height: 175px;
}
</style>
