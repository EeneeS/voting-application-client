<template>
  <Header :connected="connected"></Header>
  <router-view/>
</template>

<script setup>

import { ref } from 'vue';
import Header from "./components/Header.vue";

// CONNECTING TO THE SERVER
const ws = new WebSocket("ws://localhost:5000");
ws.onopen = function(event) {
  console.log("connection to server established.")
  connected.value = true;
}
ws.onmessage = function(event) {
  console.log(event.data);
}

const connected = ref(false);

</script>

<style>
body {
  background-color: rgb(49, 55, 61);
}
</style>
