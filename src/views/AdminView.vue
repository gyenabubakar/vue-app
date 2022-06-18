<template>
  <div class="about">
    <div class="heading">
      <div>
        <h1>{{ pageTitle }}</h1>
      </div>
      <div v-if="!$route.query.newResource">
        <button class="semibold" @click="onAddNewResource">
          {{ buttonLabel }}
        </button>
      </div>
    </div>

    <div class="content">
      <Resources
        v-if="!$route.query.newResource"
        :active-tab.sync="activeTab"
      />

      <UploadDocForm v-else />
    </div>
  </div>
</template>

<script>
// the tilde (~) is an alias to /src
import Resources from "~/components/Resources.vue";
import tabs from "~/assets/tabs";
import UploadDocForm from "~/components/UploadDocForm.vue";

export default {
  name: "AdminView",
  components: {
    Resources,
    UploadDocForm,
  },
  data() {
    return {
      activeTab: tabs[0],
    };
  },
  computed: {
    pageTitle() {
      if (this.$route.query.newResource) {
        switch (this.$route.query.newResource) {
          case "pdf":
            if (this.$route.query.edit) {
              return "Edit PDF Info";
            }
            return "Upload PDF";
          case "html-snippet":
            if (this.$route.query.edit) {
              return "Edit HTML Snippet";
            }
            return "Add HTML Snippet";
          default:
            if (this.$route.query.edit) {
              return "Edit Link";
            }
            return "Add New Link";
        }
      }
      return "Admin";
    },
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
    activeTab() {
      if (this.$route.query.newResource) {
        this.$router.push({
          query: {},
        });
      }
    },
    pageTitle(title) {
      this.$nextTick(() => {
        document.title = title;
      });
    },
  },
  mounted() {
    document.title = this.pageTitle;
  },
  methods: {
    onAddNewResource() {
      const resource = this.activeTab.id.slice(0, -1);
      this.$router.push({
        query: {
          newResource: resource,
        },
      });
    },
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
  cursor: pointer;
}

.heading button:hover {
  background: var(--main-color-dark);
}
</style>
