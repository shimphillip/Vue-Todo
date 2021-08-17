<template>
  <form @submit.prevent="addTodo">
    <fieldset>
      <input type="text" placeholder="What's on your mind?" v-model="text" />
    </fieldset>
  </form>
</template>

<script>
// Don't need separate event listener for submit in vue.
// Enter will add a new todo automatically.
export default {
  props: {
    newId: Number,
  },
  data() {
    return {
      text: "",
    };
  },
  methods: {
    addTodo() {
      if (!this.text.length) {
        return;
      }
      this.$emit("add-todo", {
        id: this.newId,
        isComplete: false,
        text: this.text,
      });
      this.text = "";
    },
  },
};
</script>

<style>
</style>