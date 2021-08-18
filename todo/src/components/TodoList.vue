<template>
  <div>
    <ul>
      <TodoItem
          v-for="(item, i) of todos"
          :item="item"
          :index="i"
          :key="item.id"
          @remove-todo="removeTodo"
      ></TodoItem>
    </ul>
  </div>
</template>


<script>
import TodoItem from "./TodoItem";

export default {
  props: ['todos'],
  components: {TodoItem},
  methods: {
    removeTodo(id) {
      this.$emit('remove-todo', id)
    }
  }
}
</script>


<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

</style>
