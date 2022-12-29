<template>
  <div class="flex flex-col text-center h-screen justify-center overflow-hidden -mt-40">
    <ul>
      <Dilemma v-if="!waitingForNetwork" :dilemma="dilemma"></Dilemma>
      <i v-if="waitingForNetwork" class="fa-solid fa-hourglass-start fa-flip fa-6x text-white" style="--fa-flip-x: 1; --fa-flip-y: 0;"></i>
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
  data() {
    return {
      dilemmas: [],
      dilemma: {},
      waitingForNetwork: true,
    }
  },
  methods: {
    async fetchDilemmas() {
      const res = await fetch("http://localhost:5001/quotes");
      const data = await res.json();
      return data;
    },
    async fetchDilemmaById(id) {
      this.waitingForNetwork = true;
      const res = await fetch(`http://localhost:5001/quotes/${id}`);
      const data = await res.json();
      this.waitingForNetwork = false;
      return data[0];
    },
    getRandomNumber() {
      return Math.floor(Math.random() * this.dilemmas.length + 1);
    }
  },
  async created() {
    this.dilemmas = await this.fetchDilemmas();
    this.dilemma = await this.fetchDilemmaById(this.getRandomNumber());
  },
}
</script>
