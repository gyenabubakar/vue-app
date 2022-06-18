<template>
  <form @submit.prevent="onSubmit" autocomplete="off">
    <div class="form-field">
      <label for="link-title">Title</label>
      <input
        id="link-title"
        type="text"
        v-model="title"
        required
        placeholder="Enter the link title"
      />
    </div>
    <div class="form-field">
      <label for="link-url">URL</label>
      <input
        id="link-url"
        type="text"
        v-model="url"
        required
        placeholder="Enter URL"
      />
    </div>
    <div class="form-field">
      <input type="checkbox" id="open-new-tab" v-model="openInNewTab" />
      <label for="open-new-tab"> Open in new tab </label>
    </div>

    <div class="btn-wrapper">
      <button type="submit" class="semibold">Upload document</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "AddLinkForm",
  data() {
    return {
      title: "",
      url: "",
      openInNewTab: false,
    };
  },
  methods: {
    onSubmit() {
      if (this.url && this.title) {
        const { title, url, openInNewTab } = this;
        // eslint-disable-next-line no-unused-vars
        const formData = {
          title,
          url,
          openInNewTab,
        };

        /* This component is used for editing and adding new content.
          So, check if there's a query param called `edit` whose value is a resource ID.
          If it exists, then we're editing an existing link. (POST)
          If it exists, then we're adding a new link. (PATCH)

          if (this.$route.query.edit) {
            try {
              await axios.patch(
                `/api/snippets/${this.$route.query.edit}`,
                formData
              )

              // --> leave the current FORM screen on success
              this.$router.push({
                query: {}
              });
            } catch (error) {
              // --> show error message
              alert('Some error');
            }
            return;
          }

          try {
            await axios.post(`/api/snippets`, formData);

            // --> leave the current FORM screen on success
            this.$router.push({
              query: {}
            });
          } catch (error) {
            // --> show error message
            alert('Some error');
          }
        */
      }
    },
  },
};
</script>

<style scoped>
form {
  width: 500px;
  margin: 0 auto;
}

.form-field {
  margin-bottom: 1.3rem;
}

.form-field label {
  font-weight: 500;
}

.btn-wrapper {
  margin-top: 50px;
  text-align: center;
}
</style>
