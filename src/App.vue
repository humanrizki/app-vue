<script>
let id = 1
export default {
  data() {
    return {
      newTodo: '',
      emptyNewTodo: false,
      openModal: false,
      modalType: '',
      editTodo: false,
      todo: null,
      todos: [
        { id: id++, text: 'Learn HTML' },
        { id: id++, text: 'Learn JavaScript' },
        { id: id++, text: 'Learn Vue Js' }
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
          this.openModal = false
        } else {
          this.emptyNewTodo = false
          this.todos.push({id:id++, text: this.newTodo})
          this.newTodo = ''
          this.openModal = false
        }
        this.openModal = false
      }
    },
    editAnyTodo(todo, key){
      this.openModal = true
      this.modalType = 'edit'
      this.newTodo = todo.text
      this.editTodo = true
      this.todoKey = key
    },
    updateTodo(){
      this.todos[this.todoKey].text = this.newTodo
      this.resetField()
      this.cancelModal()
    },
    cancelEditAnyTodo(){
      this.resetField()
    },
    removeTodo(todo) {
      // ...
      this.todos = this.todos.filter(function(value){
        return todo.id != value.id
      })
      this.resetField()
    },
    resetField(){
      this.newTodo = ''
      this.editTodo = false
      this.todoKey = null
    },
    openModalAdd(){
      this.openModal = true
      this.modalType = 'add'
    },
    cancelModal(){
      this.openModal = false
      this.modalType = ''
      this.resetField()
    }
  }
}
</script>

<template>
<div class="w-4/5 md:w-1/2 p-2 mx-auto ">
  <!-- <form @submit.prevent="updateTodo" v-if="editTodo">
    <input v-model="newTodo" class="p-2 border rounded shadow">
    <button class="p-2 border rounded shadow bg-blue-400 hover:bg-blue-500 text-white">Edit Todo</button>
    <p v-if="emptyNewTodo" class="text-sm text-red-500 font-medium">Inputan tidak boleh kosong</p>    
  </form>
  <form @submit.prevent="addTodo" v-else>
    <input v-model="newTodo" class="p-2 border rounded shadow">
    <button class="p-2 border rounded shadow bg-blue-400 hover:bg-blue-500 text-white">Add Todo</button>
    <p v-if="emptyNewTodo" class="text-sm text-red-500 font-medium">Inputan tidak boleh kosong</p>    
  </form> -->
  <button v-on:click="openModalAdd" class="p-2 border rounded shadow border-green-300 hover:bg-green-300 text-green-300 hover:text-white">Add new</button>
  
  <ol class="list-decimal list-inside"> 
    <li v-for="(todo, index) in todos" :key="index" class="p-2 my-2 shadow rounded border flex justify-between items-center">
      <p class="text-gray-700 inline text-base font-medium mr-2">{{ todo.text }}</p>
      <div class="action">
        <button @click="removeTodo(todo)" class="p-2 mr-2 border rounded shadow border-red-500 hover:bg-red-500 text-red-500 hover:text-white">Delete</button>
        <button @click="editAnyTodo(todo, index)" class="p-2 border rounded shadow border-yellow-300 hover:bg-yellow-300 text-yellow-300 hover:text-white">Edit</button>
      </div>
      
    </li>
  </ol>
</div>
<div class="fixed w-full h-full bg-gray-300 top-0 left-0 right-0 opacity-100" v-if="openModal && modalType == 'add'" >
  <div class="w-4/5 md:w-1/2 h-max rounded shadow bg-white absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 opacity-100">
    <div class="header border border-bottom p-2 rounded-t flex justify-between">
      <p>Add new Todo</p>
      <button v-on:click="cancelModal" class="h-[30px] w-[30px] text-base border rounded-full shadow border-red-500 hover:bg-red-500 text-red-500 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
    </div>
    <div class="content p-2">
      <input v-model="newTodo" class="p-2 border rounded shadow w-full">
      <p v-if="emptyNewTodo" class="text-sm text-red-500 font-medium">Inputan tidak boleh kosong</p>  
    </div>
    <div class="footer border border-top p-2 rounded-b">
      <div class="flex justify-end">
        <button v-on:click="addTodo" class="p-2 mr-2 text-base border rounded shadow border-lime-500 hover:bg-lime-500 text-lime-500 hover:text-white">Add</button>
        <button v-on:click="cancelModal" class="p-2 text-base border rounded shadow border-red-500 hover:bg-red-500 text-red-500 hover:text-white">Cancel</button>
      </div>
    </div>
  </div>
</div>
<div class="fixed w-full h-full bg-gray-300 top-0 left-0 right-0 opacity-100" v-else-if="openModal && modalType == 'edit'" >
  <div class="w-4/5 md:w-1/2 h-max rounded shadow bg-white absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 opacity-100">
    <div class="header border border-bottom p-2 rounded-t flex justify-between">
      <p>Update Todo</p>
      <button v-on:click="cancelModal" class="h-[30px] w-[30px] text-base border rounded-full shadow border-red-500 hover:bg-red-500 text-red-500 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
    </div>
    <div class="content p-2">
      <input v-model="newTodo" class="p-2 border rounded shadow w-full">
      <p v-if="emptyNewTodo" class="text-sm text-red-500 font-medium">Inputan tidak boleh kosong</p>  
    </div>
    <div class="footer border border-top p-2 rounded-b">
      <div class="flex justify-end">
        <button v-on:click="updateTodo" class="p-2 mr-2 text-base border rounded shadow border-lime-500 hover:bg-lime-500 text-lime-500 hover:text-white">Update</button>
        <button v-on:click="cancelModal" class="p-2 text-base border rounded shadow border-red-500 hover:bg-red-500 text-red-500 hover:text-white">Cancel</button>
      </div>
    </div>
  </div>
</div>
</template>

<style>
/* @import './assets/base.css'; */
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/css/all.min.css');
</style>
