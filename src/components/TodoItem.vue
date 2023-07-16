<template>
  <p :class="['todo-item', todoProps.completed ? 'is-completed' : '']">
    <input
      type="checkbox"
      :checked="todoProps.completed"
      @change="submitItemCompleted"
    />
    {{ todoProps.title }}
    <button class="btn" @click="deleteItem">Delete</button>
  </p>
</template>
<script lang="ts">
export default {
  name: "TodoItem",
  props: ["todoProps"],
  setup(props, context) {
    const submitItemCompleted = () => {
      context.emit("item-completed", props.todoProps.id);
    };
    const deleteItem = () => {
      context.emit("delete-item", props.todoProps.id);
    };
    return {
      submitItemCompleted,
      deleteItem,
    };
  },
};
</script>
<style lang="css" scoped>
.todo-item {
  background-color: #f4f4f4;
  padding: 10px;
  margin: 0px;
}
.is-completed {
  text-decoration: line-through;
}
.btn {
  background-color: red;
  color: #fff;
  cursor: pointer;
  border: 1px solid #333;
  border-radius: 4px;
  float: right;
}
.btn:hover {
  background-color: gray;
}
</style>
