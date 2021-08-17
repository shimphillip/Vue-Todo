<template>
  <li class="row">
    <div class="row" v-if="!isEditing">
      <input
        type="checkbox"
        :id="id"
        :checked="isComplete"
        @click="$emit('toggle-todo')"
      />
      <label :for="id" :class="{ completed: isComplete }">{{ text }}</label>
    </div>
    <div class="row" v-else>
      <input
        class="editor"
        type="text"
        v-model="newTodoDescription"
        @blur="finishEditing()"
        ref="newTodo"
      />
    </div>
    <button class="button button-outline purple" @click="startEditing()">
      Edit
    </button>
    <button class="button button-outline red" @click="$emit('delete-todo')">
      Delete
    </button>
  </li>
</template>

<script>
export default {
  props: {
    id: Number,
    isComplete: Boolean,
    text: String,
  },
  data() {
    return {
      isEditing: false,
      newTodoDescription: "",
    };
  },
  methods: {
    startEditing() {
      if (this.isEditing) {
        this.finishEditing();
      } else {
        this.newTodoDescription = this.text;
        this.isEditing = true;
        this.$nextTick(() => this.$refs.newTodo.focus());
      }
    },
    finishEditing() {
      this.isEditing = false;
      this.$emit("edit-todo", this.newTodoDescription);
    },
  },
};
</script>

<style scoped>
.row {
  align-items: center;
}
li.row {
  justify-content: space-between;
}
input[type="checkbox"] {
  display: flex;
  align-items: center;
  margin-bottom: 0;
  margin-right: 10px;
}

label {
  cursor: pointer;
  margin-bottom: 0;
}

.editor {
  margin-right: 10px;
  margin-bottom: 0;
}

button {
  margin-right: 5px;
  margin-bottom: 0;
}

button.purple:hover {
  color: #9b4dca;
  border-color: #9b4dca;
}

button.red {
  color: red;
  border-color: red;
}

button.red:hover {
  color: red;
  border-color: red;
  cursor: pointer;
}

.completed {
  text-decoration: line-through;
}
</style>