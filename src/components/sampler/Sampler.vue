<template>
  <div>
    <div id="sampler" ref="wrap" class="w-screen h-screen z-0"></div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import * as d3 from 'd3';

import { rgbToHex, poissonDiscSampler } from './PoissonDiscSampler';

@Component
export default class Sampler extends Vue {
  @Prop() ctx!: OffscreenCanvasRenderingContext2D;

  wrap!: HTMLDivElement;

  activate: boolean = false;

  width: number = 0;

  height: number = 0;

  numSamplesPerFrame = 50;

  sampleRadius = 7;

  timerActive = 0;

  svg: any;

  box: any;

  img: any;

  canvas: any;

  mounted() {
    this.wrap = this.$refs.wrap as HTMLDivElement;
    window.addEventListener('resize', this.handleResize);

    this.box = d3.select('#sampler').on('click', this.redraw);
    this.svg = this.box.append('svg');

    this.handleResize();
  }

  beforeDestroy() {
    window.removeEventListener('resize', this.handleResize);
  }

  handleResize() {
    this.width = this.wrap.clientWidth;
    this.height = this.wrap.clientHeight;

    this.svg
      .attr('width', this.width)
      .attr('height', this.height);

    this.$nextTick(this.redraw);
  }

  redraw() {
    const sample = poissonDiscSampler(this.width, this.height, this.sampleRadius);
    // eslint-disable-next-line
    const timer = ++this.timerActive;

    this.svg.selectAll('circle').remove();
    this.box.classed('animation--playing', true);

    // eslint-disable-next-line
    d3.timer(() => {
      if (this.timerActive !== timer) return true;
      // eslint-disable-next-line
      for (let i = 0; i < this.numSamplesPerFrame; ++i) {
        const s = sample();
        if (!s) return this.box.classed('animation--playing', false);

        /*
        let R = this.ctx.getImageData(s[0], s[1], 1, 1).data[0]/255;
        let G = this.ctx.getImageData(s[0], s[1], 1, 1).data[1]/255;
        let B = this.ctx.getImageData(s[0], s[1], 1, 1).data[2]/255;
        let A = this.ctx.getImageData(s[0], s[1], 1, 1).data[3]

        R *= 0.2126
        G *= 0.7152
        B *= 0.0722

        let C = R + G + B;
        let S;

        C <= 0.0031308 ? S = 12.92*C : S = 1.055*Math.pow(C, 1/2.4)  - 0.055
        ---------------------------------------------------------------------

        let R = (this.ctx.getImageData(s[0], s[1], 1, 1).data[0]/255)*0.2126;
        let G = (this.ctx.getImageData(s[0], s[1], 1, 1).data[1]/255)*0.7152;
        let B = (this.ctx.getImageData(s[0], s[1], 1, 1).data[2]/255)*0.0722;
        let S = R + G + B;
        */

        const R = this.ctx.getImageData(s[0], s[1], 1, 1).data[0];
        //const G = this.ctx.getImageData(s[0], s[1], 1, 1).data[0];
        //const B = this.ctx.getImageData(s[0], s[1], 1, 1).data[0];

        this.svg
          .append('circle')
          .attr('cx', s[0])
          .attr('cy', s[1])
          .attr('r', 1e-6)
          .attr('fill', rgbToHex(R, R, R))
          .transition()
          .attr('r', (1 - R / 255) * 9);
      }
    });
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
