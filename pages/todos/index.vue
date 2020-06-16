<template>
  <!-- <template>: コンポーネントのhtmlを埋め込む -->
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      <!-- v-for で 配列などプロパティに対するイテレーションを書く -->
      <!-- リストレンダリング https://jp.vuejs.org/v2/guide/list.html -->
      <!-- :key を第二引数にすることで、データの保持ができる -->
      <input type="checkbox" :checked="todo.done" @change="toggle(todo)" />
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <!-- :class="{YOUR_CLASS: boolean}" で動的にCSSを適用できる -->
      <!-- {{ }}  でVueインスタンスの要素を呼び出すことができる。 -->
      <button @click="removeTodo(todo)">remove</button>
      <!-- @ は v-on の省略記法 -->
    </li>
    <li>
      <input placeholder="What needs to be done?" @keyup.enter="addTodo" />
    </li>
  </ul>
</template>

<script>
import { mapMutations } from 'vuex'
export default {
  computed: {
    todos() {
      return this.$store.state.todos.list
    }
  },
  methods: {
    removeTodo(todo) {
      this.$store.commit('todos/remove', todo)
    },
    addTodo(e) {
      this.$store.commit('todos/add', e.target.value)
      e.target.value = ''
    },
    ...mapMutations({
      toggle: 'todos/toggle'
    })
  }
}
</script>

<style>
.done {
  text-decoration: line-through;
}
</style>
