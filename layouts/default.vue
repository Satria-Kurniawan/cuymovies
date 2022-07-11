<template>
  <div
    :style="{
      'background-image': 'url(' + `${require('assets/img/cinema.jpg')}` + ')',
      'background-size': 'auto',
    }"
  >
    <Header />
    <Nuxt />
  </div>
</template>

<script>
import Header from "../components/Header.vue";

export default {
  name: "default",
  components: {
    Header,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@100;400;500;600;700;800;900&family=Poppins:ital,wght@0,400;0,500;0,600;0,700;0,900;1,400;1,500;1,600;1,700;1,900&display=swap");

html {
  scroll-behavior: smooth;
}

div {
  font-family: "Poppins", sans-serif;
}
</style>
