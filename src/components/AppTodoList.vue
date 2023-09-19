<template>
  <ul class="todo-list">
    <AppTodoItem
      v-for="todo in todos" 
      :key="todo.id"
      :todo="todo"
      @toggle-todo="toggleTodo"
      />
  </ul>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import AppTodoItem from './AppTodoItem.vue'
import { Todo } from '../types/Todo'

interface State {
  todos: Todo[]
}

export default defineComponent({
  components: {
    AppTodoItem
  },
  data(): State {
    return {
      todos: [
        { id: 0, text: 'Learn the basics of Vue', completed: true },
        { id: 1, text: 'Learn the basics of Typescript', completed: false },
        { id: 2, text: 'Subscribe to the channel', completed: false }
      ]
    }
  },
  methods: {
    toggleTodo(id: number) {
      // Ищем в массиве todos нужный объект todo по id
      // (todo: Todo) - говорит что todo это объект типа Todo. Можно написать просто todo.
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id)
      // Если targetTodo найдено, то свойство completed переключится на противоположное значение
      if(targetTodo) {
        targetTodo.completed = !targetTodo.completed
      }
    }
  }
})
</script>