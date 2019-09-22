<template>
  <div id="app">
    <Sampler v-bind:ctx="ctx" v-if="ready" ref="sampler" class="absolute overflow-hidden z-0" />
    <Banner v-if="ready" @entered="complete" class="relative overflow-hidden z-10" />
    <Background v-bind:url="urlx" @loaded="load" hidden />
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

  start: boolean = false;
  
  url!: string;

  ctx: any;

  urls = [
    "https://images.unsplash.com/photo-1501785888041-af3ef285b470?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80",
    "https://images.unsplash.com/photo-1506744038136-46273834b3fb?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80",
    "https://images.unsplash.com/photo-1532274402911-5a369e4c4bb5?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80",
    "https://images.unsplash.com/photo-1524260855046-f743b3cdad07?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2001&q=80",
    "https://images.unsplash.com/photo-1504217051514-96afa06398be?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2134&q=80",
    "https://images.unsplash.com/photo-1472214103451-9374bd1c798e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80",
    "https://images.unsplash.com/photo-1501791330673-603715379ded?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80",
    "https://images.unsplash.com/photo-1419064642531-e575728395f2?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80"
  ]

  complete() {
    this.completed = true;
  }

  load(e: OffscreenCanvasRenderingContext2D) {
    this.ready = true;
    this.ctx = e;
  }

  get urlx() {
    this.url = this.urls[Math.floor(Math.random()*this.urls.length)];
    console.log(this.url);
    return  this.url;
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
