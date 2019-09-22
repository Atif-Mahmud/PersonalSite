<template>
  <transition appear v-on:after-enter="() => this.$emit('entered')" name="box">
    <div
      v-if="reveal"
      class="max-w-sm md:max-w-md lg:max-w-full mx-auto mt-2 p-6 rounded-lg shadow-2xl"
      style="backdrop-filter: blur(5px); -webkit-backdrop-filter: blur(5px); background-color: rgba(0, 0, 0, 0.5"
    >
      <transition appear v-on:after-enter="() => this.$emit('after')" name="contents">
        <slot></slot>
      </transition>
    </div>
  </transition>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Box extends Vue {
  @Prop() reveal!: boolean;
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* Enter and leave animations can use different */
/* durations and timing functions.              */

.box-enter-active {
  animation: special 1s ease;
}

.contents-enter-active {
  transition: all 0.3s ease 0.8s;
}

.contents-enter {
  transform: translateY(10px);
  opacity: 0;
  /*filter: blur(10px);*/
  /*-webkit-filter: blur(10px);*/
}

@keyframes special {
  0% {
    transform: translateY(var(--direction));
    transform: scale(0);
    padding: 0 0 0 0;
    opacity: 0;
  }

  70% {
    transform: scaleY(1);
    transform: scaleX(0.05);
  }
}
</style>
