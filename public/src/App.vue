<template>
  <div id="app" class="container mt-4 pt-4">
    <div class="text-center">
      <img src="./assets/logo.png" class="mb-4">
    </div>
    <ContactForm/>
  </div>
</template>

<script>
import ContactForm from "./components/ContactForm.vue";
export default {
  name: "app",
  components: {
    ContactForm
  }
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
