<script>
let id = 1
export default {
  data() {
    return {
      newTodo: '',
      emptyNewTodo: false,
      editTodo: false,
      todos: [
        { id: id++, text: 'Learn HTML' },
        { id: id++, text: 'Learn JavaScript' },
        { id: id++, text: 'Learn Vue' }
      ]
    }
  },
  methods: {
    addTodo() {
      // ...
      if(this.newTodo == ''){
        this.emptyNewTodo = true
      } else {
        if(this.todos.length == 0){
          id = 1
          this.emptyNewTodo = false
          this.todos.push({id:id++, text: this.newTodo})
          this.newTodo = ''
        } else {
          this.emptyNewTodo = false
          this.todos.push({id:id++, text: this.newTodo})
          this.newTodo = ''
        }
        
      }
    },
    editAnyTodo(todo){
      this.newTodo = todo.text
      this.editTodo = true
    },
    updateTodo(todo){

    },
    removeTodo(todo) {
      // ...
      this.todos = this.todos.filter(function(value){
        return todo.id != value.id
      })
    }
  }
}
</script>

<template>
<div class="container p-2 ">
  
  <form @submit.prevent="addTodo" v-if="editTodo">
    <input v-model="newTodo" class="p-2 border rounded shadow">
    <button class="p-2 border rounded shadow bg-blue-400 hover:bg-blue-500 text-white">Add Todo</button>
    <p v-if="emptyNewTodo" class="text-sm text-red-500 font-medium">Inputan tidak boleh kosong</p>    
  </form>
  <form @submit.prevent="updateTodo" v-else>
    <input v-model="newTodo" class="p-2 border rounded shadow">
    <button class="p-2 border rounded shadow bg-blue-400 hover:bg-blue-500 text-white">Add Todo</button>
    <p v-if="emptyNewTodo" class="text-sm text-red-500 font-medium">Inputan tidak boleh kosong</p>    
  </form>
  <ul > 
    <li v-for="todo in todos" :key="todo.id">
      <p class="text-gray-700 inline text-base font-medium mr-2">{{todo.id}}. {{ todo.text }}</p>
      <button @click="removeTodo(todo)" class="p-2 border rounded shadow border-red-500 hover:bg-red-500 text-red-500 hover:text-white">X</button>
      <button @click="editAnyTodo(todo)" class="p-2 border rounded shadow border-red-500 hover:bg-red-500 text-red-500 hover:text-white">E</button>
    </li>
  </ul>
</div>
  
</template>

<style>
/* @import './assets/base.css'; */
</style>
