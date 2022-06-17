<template>
  <div class="home">
    <h1 class="extrabold">Home</h1>

    <div class="content">
      <Resources :active-tab.sync="activeTab" />
    </div>
  </div>
</template>

<script>
// the tilde (~) is an alias to /src
import Resources from "~/components/Resources.vue";
import tabs from "~/assets/tabs";

export default {
  name: "HomeView",
  components: {
    Resources,
  },
  data() {
    return {
      activeTab: tabs[0],
    };
  },
  mounted() {
    document.title = "Home";
  },
};
</script>
