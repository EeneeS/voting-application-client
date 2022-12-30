<template>
  <div class="flex flex-col text-center md:h-screen justify-center overflow-hidden md:-mt-40 mt-8">
    <ul>
      <Dilemma></Dilemma>
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
