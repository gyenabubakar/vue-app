<template>
  <div class="resources">
    <Tabs v-if="currentTab" :tabs="tabs" :active-tab.sync="currentTab" />

    <div
      class="resources-list grid"
      :class="{
        'grid-cols-2': currentTab === 'html-snippets',
        'grid-cols-3': ['pdfs', 'links'].includes(currentTab.id),
      }"
    >
      <template v-if="currentTab.id === 'links'">
        <LinkCard
          v-for="link in fakeLinks"
          :key="link.id"
          :link="link"
          :on-admin-route="onAdminRoute"
        />
      </template>
      <template v-else-if="currentTab.id === 'html-snippets'">
        <CodeSnippetCard
          v-for="snippet in fakeHtmlSnippets"
          :key="snippet.id"
          :snippet="snippet"
          :on-admin-route="onAdminRoute"
        />
      </template>
      <template v-else>
        <PdfCard
          v-for="pdf in fakePdfs"
          :key="pdf.id"
          :pdf="pdf"
          :on-admin-route="onAdminRoute"
        />
      </template>
    </div>
  </div>
</template>

<script>
import Tabs from "~/components/Tabs.vue";
import tabs from "~/assets/tabs";
import LinkCard from "~/components/LinkCard.vue";
import PdfCard from "~/components/PdfCard.vue";
import CodeSnippetCard from "~/components/CodeSnippetCard.vue";

export default {
  name: "Resources",
  components: {
    Tabs,
    LinkCard,
    PdfCard,
    CodeSnippetCard,
  },
  props: {
    activeTab: {
      type: Object,
      required: true,
    },
    onAdminRoute: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      tabs,
      currentTab: null,

      links: [],
      htmlSnippets: [],
      pdfs: [],

      fakeLinks: [
        {
          id: 1,
          title: "Some Link",
          url: "https://www.google.com",
          shouldOpenInNewTab: true,
        },
        {
          id: 2,
          title: "Another Link",
          url: "https://www.google.com",
          shouldOpenInNewTab: false,
        },
      ],
      fakeHtmlSnippets: [
        {
          id: 1,
          title: "Some HTML Snippet",
          description: "Some description",
          html: "<h1>Some HTML Snippet</h1>",
        },
        {
          id: 2,
          title: "Another HTML Snippet",
          description: "Some description",
          html: "<h1>Another HTML Snippet</h1>",
        },
      ],
      fakePdfs: [
        {
          id: 1,
          title: "Some PDF",
          pdf: "https://www.google.com",
        },
        {
          id: 2,
          title: "Another PDF",
          pdf: "https://www.google.com",
        },
      ],
    };
  },
  watch: {
    currentTab(tab) {
      this.$emit("update:activeTab", tab);
    },
  },
  created() {
    this.currentTab = this.activeTab;

    // perform axios request to fetch all resources depending on current tab
    /*
      switch (this.currentTab.id) {
        case "links":
          axios.get("/api/links").then(({ data }) => {
            this.links = data;
          });
          break;
        case "html-snippets":
          axios.get("/api/html-snippets").then(({ data }) => {
            this.htmlSnippets = data;
          });
          break;
        default:
          axios.get("/api/pdfs").then(({ data }) => {
            this.pdfs = data;
          });
          break;
      }
    */
  },
};
</script>

<style scoped>
.resources-list {
  margin-top: 2rem;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  grid-gap: 2rem;
}
.grid-cols-2 {
  grid-template-columns: repeat(2, minmax(250px, 1fr));
}
.grid-cols-3 {
  grid-template-columns: repeat(3, minmax(250px, 1fr));
}
</style>
