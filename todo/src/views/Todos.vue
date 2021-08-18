<template>
  <div>
    <h2>Todo application</h2>
    <router-link to="/">Home</router-link>
    <hr>

    <Loader v-if="loading"></Loader>

    <template v-else>
      <AddTodo @create-item="createItem"></AddTodo>

      <select v-model="filter">
        <option value="all">all</option>
        <option value="completed">completed</option>
        <option value="not-completed">Note completed</option>
      </select>
      <hr>
      <TodoList
          v-if="filteredTodos.length"
          :todos="filteredTodos"
          @remove-todo="removeTodo"
      ></TodoList>
      <p v-else>No todos</p>

    </template>

  </div>
</template>


<script>

import TodoList from "./../components/TodoList";
import AddTodo from "./../components/AddTodo";
import Loader from "../components/Loader";

export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  // watch: {
  //   filter(v) {
  //     console.log(v)
  //   }
  // },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos
      }
      if (this.filter === 'completed') {
        return this.todos.filter(i => i.completed)
      }
      return this.todos.filter(i => !i.completed)

    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
        .then(r => r.json())
        .then(r => {
          setTimeout(() => {
            this.todos = r;
            this.loading = false
          }, 2000)
        })
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(i => i.id !== id)
    },
    createItem(title) {
      console.log(title);
      this.todos.push({
        id: Date.now(),
        title: title,
        completed: false
      })
    }
  },
  components: {Loader, AddTodo, TodoList}
}
</script>
