<template>
  <div>
    <ol>
      <li v-for="(todoItem, index) in list" :key="index">
        <input type="checkbox" :value="todoItem.status === 'done'"
          @change="changeStatus(todoItem, $event)">{{todoItem.name}}
      </li>
    </ol>
  </div>
</template>

<script lang="ts">
import {Vue, Component} from 'vue-property-decorator'
import Todo from '../modules/Todo'

@Component({
  props: {
    list: Array
  }
})

export default class TodoList extends Vue{
  changeStatus(todoItem: Todo, e: Event) {
    let checked = (<HTMLInputElement>e.target).checked
    this.$emit('updateTodo', todoItem, {status: checked ? 'done' : 'todo'})
  }
}
</script>

<style lang="scss" scoped>

</style>
