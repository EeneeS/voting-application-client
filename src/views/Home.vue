<template>
  <div class="flex flex-col text-center h-screen justify-center overflow-hidden -mt-40">
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
