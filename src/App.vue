<template>
  <AppHeader />
  <AppFilters />

  <main class="app-main">
    <AppTodoList 
      :todos="todos" 
      @toggle-todo="toggleTodo" 
      @remove-todo="removeTodo" 
    />
    <AppAddTodo @add-todo="addTodo"/>
  </main>

  <AppFooter />
</template>

<script lang="ts">
import { defineComponent } from "vue"
import AppHeader from "./components/AppHeader.vue"
import AppFilters from "./components/AppFilters.vue"
import AppTodoList from "./components/AppTodoList.vue"
import AppAddTodo from "./components/AppAddTodo.vue"
import AppFooter from "./components/AppFooter.vue"
import { Todo } from "./types/Todo"

interface State {
  todos: Todo[]
}

export default defineComponent({
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter
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
    addTodo(todo: Todo) {
      this.todos.push(todo)
    },
    toggleTodo(id: number) {
      // Ищем в массиве todos нужный объект todo по id
      // (todo: Todo) - говорит что todo это объект типа Todo. Можно написать просто todo.
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id)
      // Если targetTodo найдено, то свойство completed переключится на противоположное значение
      if(targetTodo) {
        targetTodo.completed = !targetTodo.completed
      }
    },
    removeTodo(id: number) {
      // Новый массив будет состоять из элементов, чей id не совпадает с id аргумента
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id)
    }
  }
})
</script>