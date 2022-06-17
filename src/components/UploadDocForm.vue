<template>
  <form @submit.prevent="onSubmit">
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
        <button v-if="file" class="semibold" @click="onRemoveFile">
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
    };
  },
  methods: {
    onRemoveFile() {
      this.file = null;
      this.$refs.fileInput.value = "";
    },
    onFileChange(e) {
      this.file = e.target.files[0];
    },
    onSubmit() {
      if (this.file && this.title) {
        this.$emit("submit", {
          title: this.title,
          file: this.file,
        });
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
  margin-bottom: 1rem;
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
