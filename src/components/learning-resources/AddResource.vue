<template>
  <base-dialog v-if="inputIsInvalid" @close="confirmError" title="Invalid Input">
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>Please make sure to enter at least a few characters on each input!</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="addResource" ref="resourceForm">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="titleInput">
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea id="description" name="description" rows="3" ref="descInput"></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="linkInput">
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  inject: ['addItem'],
  data() {
    return {
      inputIsInvalid: false
    };
  },
  methods: {
    addResource() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredLink = this.$refs.linkInput.value;
      if (enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredLink.trim() === '') {
        this.inputIsInvalid = true;
      } else {
        const newResource = {
          title: enteredTitle,
          description: enteredDescription,
          link: enteredLink
        };
        this.addItem(newResource);
        this.$refs.resourceForm.reset();
      }
    },
    confirmError() {
      this.inputIsInvalid = false;
    }
  }
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
