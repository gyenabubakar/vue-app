<template>
  <form @submit.prevent="onSubmit" autocomplete="off">
    <div class="form-field">
      <label for="pdf-title">Title</label>
      <input
        id="pdf-title"
        type="text"
        v-model="title"
        required
        placeholder="Enter a title for your PDF"
      />
    </div>
    <div class="form-field file">
      <div>
        <label for="pdf-file">Choose PDF document</label>
        <button
          v-if="file || existingPdfUrl"
          class="semibold"
          @click="onRemoveFile"
        >
          Remove
        </button>
      </div>
      <input
        ref="fileInput"
        id="pdf-file"
        type="file"
        accept=".pdf"
        required
        placeholder="Choose a file"
        @change="onFileChange"
      />
    </div>

    <div class="btn-wrapper">
      <button type="submit" class="semibold">Upload document</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "UploadDocForm",
  data() {
    return {
      title: "",
      file: null,
      existingPdfUrl: null,
    };
  },
  created() {
    /* Check if there's a query param called `edit` whose value is a PDF ID.
     * If it exists, then we're editing an existing PDF, so fetch it's data and populate the form.

      if (this.$route.query.edit) {
        const linkId = this.$route.query.edit;
        axios
          .get(`/api/links/${linkId}`)
          .then((response) => {
            const pdf = response.data;
            this.title = pdf.title;
            this.existingPdfUrl = pdf.url;
          })
          .catch((error) => {
            //  --> show error
          });
      }

    */
  },
  methods: {
    onRemoveFile() {
      this.file = null;
      this.$refs.fileInput.value = "";
      this.existingPdfUrl = null;
    },
    onFileChange(e) {
      this.file = e.target.files[0];
    },
    onSubmit() {
      if ((this.file || this.existingPdfUrl) && this.title) {
        const { title, file } = this;
        const formData = new FormData();
        formData.append("title", title);
        // appending file only if it exists
        if (this.file) {
          formData.append("file", file);
        }

        /* This component is used for editing and adding new content.
         * So, check if there's a query param called `edit` whose value is a resource ID.
         * If it exists, then we're editing an existing PDF file. (POST)
         * If it exists, then we're adding a new PDF file. (PATCH)

          if (this.$route.query.edit) {
            try {
              await axios.patch(
                `/api/snippets/${this.$route.query.edit}`,
                formData,
                {
                  headers: {
                    "Content-Type": "multipart/form-data",
                  },
                }
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

.form-field.file > div {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-field.file > div > button {
  color: var(--main-color);
  background: transparent;
  border: 0;
  outline: 0;
}
.form-field.file > div > button:hover {
  color: var(--main-color-dark);
}

.btn-wrapper {
  margin-top: 50px;
  text-align: center;
}

.btn-wrapper button {
  border: 0;
  outline: 0;
  padding: 10px 35px;
  border-radius: 25px;
  background: var(--main-color);
  color: white;
  cursor: pointer;
}

.btn-wrapper button:hover {
  background: var(--main-color-dark);
}
</style>
