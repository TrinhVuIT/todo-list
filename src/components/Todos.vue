<template>
  <AddTodo @add-todo="addTodo" />
  <TodoItem
    v-for="todo in todos"
    :key="todo.id"
    :todoProps="todo"
    @item-completed="submitCompleted"
    @delete-item="deleteTodo"
  />
</template>
<script lang="ts">
import { ref } from "vue";
import { uuid } from "vue-uuid";
// import axios from "axios";
import TodoItem from "./TodoItem.vue";
import AddTodo from "./AddTodo.vue";
export default {
  name: "Todos",
  components: { TodoItem, AddTodo },
  setup() {
    const todos = ref([
      {
        id: uuid.v4(),
        title: "Việc 1",
        completed: false,
      },
      {
        id: uuid.v4(),
        title: "Việc 2",
        completed: true,
      },
      {
        id: uuid.v4(),
        title: "Việc 3",
        completed: false,
      },
    ]);

    // const getAllTodo = async () => {
    //   try {
    //     const res = await axios.get(
    //       "https://jsonplaceholder.typicode.com/todos?_limit=5"
    //     );
    //     todos.value = res.data;
    //   } catch (error) {
    //     console.log(error);
    //   }
    // };
    // getAllTodo();

    const submitCompleted = (id: string) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id === id) {
          todo.completed = !todo.completed;
        }
        return todo;
      });
    };

    const deleteTodo = (id: string) => {
      //   try {
      //     await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
      //     todos.value = todos.value.filter((todo) => todo.id != id);
      //   } catch (error) {
      //     console.log(error);
      //   }
      todos.value = todos.value.filter((todo) => todo.id != id);
    };

    const addTodo = async (newTodo: any) => {
      //   try {
      //     const res = await axios.post(
      //       "https://jsonplaceholder.typicode.com/todos",
      //       newTodo
      //     );
      //     todos.value.push(res.data);
      //   } catch (error) {
      //     console.log(error);
      //   }
      todos.value.push(newTodo);
    };
    return {
      todos,
      submitCompleted,
      deleteTodo,
      addTodo,
    };
  },
};
</script>

<style lang=""></style>
