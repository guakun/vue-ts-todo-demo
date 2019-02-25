<template>
  <div class="app">
    <div class="inner">
      <new-todo @addTodo="addTodo"></new-todo>
      <todo-list :list="list" @updateTodo="updateTodo"></todo-list>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import NewTodo from './components/NewTodo.vue'
import TodoList from './components/TodoList.vue'
import Todo from './modules/Todo'

@Component({
  components: {
    NewTodo, TodoList
  },
  watch: {
    list(newValue: Array<Todo>) {
      let string = JSON.stringify(newValue)
      localStorage.setItem('list', string)
    }
  }
})
export default class App extends Vue {
  list: Array<Todo> = localStorage.getItem('list') ? JSON.parse(<string>localStorage.getItem('list')) : []
  addTodo(name: String) {
    let todo:Todo = {name, status: 'todo'}
    this.list.push(todo)
  }
  updateTodo(todo: Todo, part: Partial<Todo>) {
    let index: number = this.list.indexOf(todo)
    let newTodo: Todo = Object.assign(todo, part)
    this.list.splice(index, 1, newTodo)
  }
}
</script>

<style lang="scss">
* {margin: 0; padding: 0;}
ul, ol { list-style: none; }
.app {
  font-family: -apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB','Microsoft YaHei','Helvetica Neue',Helvetica,Arial,sans-serif,'Apple Color Emoji','Segoe UI Emoji','Segoe UI Symbol';
  display: flex; justify-content: center; align-items: center;
  .inner {
    border: 1px solid #ddd;
    padding: 20px;
  }
}
</style>
