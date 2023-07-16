<template>
  <form @submit="addItem">
    <input type="text" placeholder="Thêm việc cần làm..." v-model="title" />
    <input type="submit" value="Thêm" class="add-btn" />
  </form>
</template>
<script lang="ts">
import { ref } from "vue";
import { uuid } from "vue-uuid";
export default {
  name: "AddTodo",
  setup(props, context) {
    const title = ref("");
    const addItem = (event: { preventDefault: () => void }) => {
      event.preventDefault();
      const newItem = {
        id: uuid.v4(),
        title: title.value,
        completed: false,
      };
      context.emit("add-todo", newItem);
      title.value = "";
    };
    return {
      title,
      addItem,
    };
  },
};
</script>
<style lang="css" scoped>
form {
  width: 100%;
  padding: 10px;
  background-color: grey;
}
input[type="text"] {
  background-color: #fff;
  padding: 5px;
  width: 70%;
  border-radius: 5px;
}
.add-btn {
  background-color: #f4f4f4;
  color: rebeccapurple;
  padding: 5px;
  margin-left: 5%;
  width: 20%;
  border-radius: 5px;
}
.add-btn:hover {
  background-color: rebeccapurple;
  color: #fff;
}
</style>
