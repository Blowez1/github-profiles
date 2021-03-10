<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-12">
        <profile></profile>
      </div>
    </div>
  </div>
</template>

<script>
import Profile from "./Profile";

export default {
  name: "app",
  components: {
    profile: Profile,
  },
};
</script>

<style lang="scss">
body {
  background-color: #00bfb2;
  background-image: linear-gradient(90deg, #00bfb2 0%, #028090 74%);
  font-family: "Montserrat", sans-serif;
}
</style>