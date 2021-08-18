<template>
  <li>
    <span :class="{done: item.completed}">
      <input type="checkbox" @change="item.completed = !item.completed">
      <strong>{{ index + 1 }}</strong>
      {{ item.title | uppercase }}
    </span>
    <button class="rm"
            @click="$emit('remove-todo', item.id)">&times;
    </button>
  </li>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    uppercase(v) {
      return v.toUpperCase()
    }
  }
}
</script>


<style scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: .5rem 2rem;
  margin-bottom: 1rem;
}

.rm {
  background-color: red;
  color: #fff;
  border-radius: 50%;
  font-weight: bold;
  width: 30px;
  height: 30px;
}

input {
  margin-right: 1rem;
}

.done {
  text-decoration: line-through;
}
</style>
