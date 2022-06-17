<template>
  <div class="about">
    <div class="heading">
      <div>
        <h1>Admin</h1>
      </div>
      <div>
        <button class="semibold">{{ buttonLabel }}</button>
      </div>
    </div>

    <div class="content">
      <Tabs :tabs="tabs" :active-tab.sync="activeTab" />
    </div>
  </div>
</template>

<script>
// the tilde (~) is an alias to /src
import Tabs from "~/components/Tabs.vue";

const tabs = [
  {
    id: "pdfs",
    name: "PDF Files",
  },
  {
    id: "html-snippets",
    name: "HTML Snippets",
  },
  {
    id: "links",
    name: "Links",
  },
];

export default {
  name: "AdminView",
  components: { Tabs },
  data() {
    return {
      tabs,
      activeTab: tabs[0],
    };
  },
  computed: {
    buttonLabel() {
      switch (this.activeTab.id) {
        case "pdfs":
          return "Upload PDF";
        case "html-snippets":
          return "Add New HTML Snippet";
        default:
          return "Add New Link";
      }
    },
  },
  watch: {
    activeTab(tab) {
      console.log(tab);
    },
  },
  mounted() {
    document.title = "Admin";
  },
};
</script>

<style scoped>
.heading {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.heading button {
  border: 0;
  outline: 0;
  padding: 10px 35px;
  border-radius: 25px;
  background: var(--main-color);
  color: white;
}
</style>
