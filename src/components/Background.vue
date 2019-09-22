<template>
  <canvas id="atif-canvas"></canvas>
</template>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";
import drawImageProp from "./sampler/CoverCanvas";

@Component
export default class Background extends Vue {
  @Prop() url!: string;

  wrap!: HTMLDivElement;

  canvas!: HTMLCanvasElement;

  ctx!: CanvasRenderingContext2D;

  mounted() {
    window.addEventListener("resize", this.handleResize);
    this.canvas = document.getElementById('atif-canvas') as HTMLCanvasElement;
    this.ctx = this.canvas.getContext(
      "2d",
    ) as CanvasRenderingContext2D;
    this.handleResize();
  }

  beforeDestroy() {
    window.removeEventListener("resize", this.handleResize);
  }

  handleResize() {
    this.canvas.height = window.innerHeight;
    this.canvas.width = window.innerWidth;
    this.$nextTick(async () => {
      this.ctx = await drawImageProp(
        this.url,
        this.ctx,
        0,
        0,
        window.innerWidth,
        window.innerHeight,
        0,
        0,
      );
      this.$emit("loaded", this.ctx);
    });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
