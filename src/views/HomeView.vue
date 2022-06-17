<template>
  <div class="home">
    <h1 class="extrabold">Home</h1>
  </div>
</template>

<script>
// the tilde (~) is an alias to /src

export default {
  name: "HomeView",
  components: {},
  mounted() {
    document.title = "Home";
  },
};
</script>
