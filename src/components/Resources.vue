<template>
  <div class="resources">
    <Tabs v-if="currentTab" :tabs="tabs" :active-tab.sync="currentTab" />
  </div>
</template>

<script>
import Tabs from "~/components/Tabs.vue";
import tabs from "~/assets/tabs";

export default {
  name: "Resources",
  components: {
    Tabs,
  },
  props: {
    activeTab: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      tabs,
      currentTab: null,
    };
  },
  watch: {
    currentTab(tab) {
      this.$emit("update:activeTab", tab);
    },
  },
  created() {
    this.currentTab = this.activeTab;
  },
};
</script>

<style></style>
