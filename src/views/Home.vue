<template>
  <div class="flex flex-col text-center h-screen justify-center overflow-hidden -mt-40">
    <ul>
      <Dilemma></Dilemma>
      <!-- <i v-if="waitingForNetwork" class="fa-solid fa-hourglass-start fa-flip fa-6x text-white" style="--fa-flip-x: 1; --fa-flip-y: 0;"></i> -->
    </ul>
  </div>
</template>

<script>
import Dilemma from "../components/Dilemma.vue";
export default {
  name: "Home",
  components: {
    Dilemma,
  },
}
</script>
