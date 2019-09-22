<template>
  <div class="flex flex-col mx-auto justify-center h-screen">
    <Box v-bind:reveal="show1" @entered="() => show2 = true">
      <h2 class="text-xl">
        Reload:
        <a href="https://www.cs.ubc.ca/~rbridson/docs/bridson-siggraph07-poissondisk.pdf" class="font-bold underline icon">Poisson Disc Distribution</a>
      </h2>
    </Box>
    <Box v-bind:reveal="true" @entered="() => show = true">
      <div>
        <img class="h-56 w-56 object-cover rounded-full mx-auto" src="../assets/jpg/avatar.jpg" />
        <div class="text-center">
          <h2 class="text-3xl md:text-6xl">
            <span class="font-bold">Atif</span>
            <span class="font-hairline">Mahmud</span>
          </h2>
          <div class="md:text-2xl">
            <a href="https://www.ibm.com/watson" class="underline icon">IBM Watson</a> |
            <a
              href="https://www.schulichleaders.com/atif-mahmud"
              class="underline icon"
            >Schulich Scholar</a>
          </div>
          <div class="md:text-2xl">Undergraduate Researcher</div>
          <div class="md:text-2xl">UWaterloo Software Engineering + C&O</div>
          <div class="text-white">atif.mahmud@uwaterloo.ca</div>
          <div class="text-white">(226) 606-9535</div>
        </div>
      </div>
    </Box>
    <Box v-bind:reveal="show" @entered="entered">
      <div class="flex flex-row justify-center">
        <a href="http://github.com/Atif-Mahmud">
          <svg
            class="h-10 w-10 icon object-center my-auto mx-2 md:mx-4"
            fill="white"
            role="img"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <title>GitHub icon</title>
            <path
              d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"
            />
          </svg>
        </a>
        <a href="http://linkedin.com/in/Atif-Mahmud">
          <img
            class="h-10 w-10 icon object-center hover: my-auto mx-2 md:mx-4"
            src="../assets/svg/linkedin.svg"
          />
        </a>
        <a href="https://keybase.io/atifmahmud">
          <img
            class="h-10 w-10 icon object-center hover: my-auto mx-2 md:mx-4"
            src="../assets/svg/icon-key.svg"
          />
        </a>
        <a href="mailto:atif.mahmud@uwaterloo.ca">
          <img
            class="h-10 w-10 icon object-center hover: my-auto mx-2 md:mx-4"
            src="../assets/svg/icon-mail.svg"
          />
        </a>
        <img
          class="h-10 w-10 icon object-center hover: my-auto mx-2 md:mx-4"
          src="../assets/svg/icon-file.svg"
        />
      </div>
    </Box>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import Box from "./Box.vue";

@Component({
  components: {
    Box,
  },
})
export default class Banner extends Vue {
  show = false;

  show1 = false;

  entered() {
    this.show1 = true;
    this.$emit("entered");
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.icon {
  transition: filter 0.3s ease;
}

.icon:hover {
  filter: invert(1);
  transform: translateY(-2px);
}
</style>
