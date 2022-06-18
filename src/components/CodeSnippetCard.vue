<template>
  <div class="link-card card">
    <h3 class="card-title">
      {{ snippet.title }}
    </h3>

    <span class="description">
      {{ snippet.description }}
    </span>

    <pre>
      <code v-text="snippet.html"></code>
    </pre>

    <div v-if="onAdminRoute" class="card-footer">
      <button @click="onEdit">Edit</button>
      <button @click="onDelete">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "CodeSnippetCard",
  props: {
    snippet: {
      type: Object,
      required: true,
      // must have these properties: id, title, description, html
    },
    onAdminRoute: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    onEdit() {
      this.$router.push({
        query: {
          newResource: "html-snippet",
          edit: this.snippet.id,
        },
      });
    },
    onDelete() {
      const confirmed = confirm(
        "Are you sure you want to delete this snippet?"
      );
      if (confirmed) {
        /* axios.delete(`/api/links/${this.link.id}`).then(() => {
          this.$emit("deleted", this.link.id);
        }); */
      }
    },
  },
};
</script>

<style scoped>
.card-footer button:first-child {
  margin-right: 10px;
}

span {
  display: block;
  margin: 5px;
  color: gray;
}

pre {
  margin: 0;
}

code {
  font-family: "Fira Code", monospace;
  font-size: 0.9em;
  background: #2d2d2d;
  padding: 10px 15px;
  color: white;
  width: 100%;
  display: block;
  border-radius: 10px;
}
</style>
