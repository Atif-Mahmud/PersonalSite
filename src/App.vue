<template>
  <div id="app">
    <Sampler v-bind:ctx="ctx" v-if="ready" ref="sampler" class="absolute overflow-hidden z-0" />
    <Banner v-if="ready" @entered="complete" class="relative overflow-hidden z-10" />
    <Background v-bind:url="url" @loaded="load" hidden />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Banner from "./components/Banner.vue";
import Background from "./components/Background.vue";
import Sampler from "./components/sampler/Sampler.vue";
import "./assets/css/main.css";

@Component({
  components: {
    Banner,
    Background,
    Sampler,
  },
})
export default class App extends Vue {
  completed: boolean = false;

  ready: boolean = false;

  ctx: any;

  url =
    "https://images.unsplash.com/photo-1501785888041-af3ef285b470?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80";

  complete() {
    this.completed = true;
  }

  load(e: OffscreenCanvasRenderingContext2D) {
    this.ready = true;
    this.ctx = e;
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Lato&display=swap");

#app {
  font-family: "Lato", "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: whitesmoke;
}
</style>
