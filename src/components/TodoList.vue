<template>
  <div>
    <p>Completed Tasks: {{todos.filter((todo) => { return todo.done === true;}).length}}</p>
    <p>Pending Tasks:: {{todos.filter((todo) => { return todo.done === false;}).length}}</p>
    <add-todo v-on:add-todo="addTodo"></add-todo>
    <todo v-for="todo in todos" v-bind:todo="todo" :key="todo.title" v-on:delete-todo="deleteTodo" v-on:change-status="changeStatusTodo"></todo>
  </div>
</template>

<script>
  import Todo from "./Todo";
  import AddTodo from "./AddTodo";

  export default {
    name: "TodoList",
    components: {AddTodo, Todo},
    props: ['todos'],
    methods: {
      deleteTodo(todo) {
        const todoIndex = this.todos.indexOf(todo);
        this.todos.splice(todoIndex, 1);
      },
      addTodo(todo) {
        this.todos.push(todo);
      },
      changeStatusTodo(todo)  {
        const todoIndex = this.todos.indexOf(todo);
        this.todos[todoIndex].done = !this.todos[todoIndex].done;
      }
    }
  }
</script>

<style scoped>

</style>
