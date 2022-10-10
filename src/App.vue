<template>
  <div class="flex justify-center pt-6 ">
    <div class="block bg-white p-5">
      <AddTodosItem v-on:add-newToo-event="addNewTodoItems" v-on:edit-item-event="editItemEvents" v-bind:editItems="editItem"/>
      <div>
        <Todos v-bind:todoData="todoData" v-on:del-todo-events="deleteTodoItem" v-on:edit-Todo-event="editTodoItem" />
      </div>
    </div>
  </div>
  
</template>

<script>

  import Todos from "./components/Todos";
  import AddTodosItem from "./components/AddTodosItem";
  import './assets/tailwind.css'

export default {
  name: 'App',
  components: {
    Todos,
    AddTodosItem
  },
  data () {
    return {
      todoData: [],
      editItem: {
        title: '',
        id: ''
      }
    }
  },
  methods: {
    addNewTodoItems(newTodo){
      
        this.todoData = [...this.todoData, newTodo];
      
    },
    deleteTodoItem(id){
      this.todoData = this.todoData.filter(tododata => tododata.id !== id);
    },
    editTodoItem(id){
      
      let objIndex = this.todoData.findIndex(obj=> obj.id === id);
      this.editItem.title = this.todoData[objIndex].title;
      this.editItem.id = id;
    },
    editItemEvents(TheToDoItem){
      let objIndex = this.todoData.findIndex(obj => obj.id === TheToDoItem.id)
      this.todoData[objIndex].title = TheToDoItem.title;
    }
  },
  watch: {
    todoData: {
      handler() {
        localStorage.setItem('todoData',JSON.stringify(this.todoData))
      },
      deep: true
    }
  },
  mounted() {
    if (localStorage.getItem("todoData")){
      this.todoData = JSON.parse(localStorage.getItem("todoData"))
    }
  }
}
</script>

<style>
  

  body{
    background: rgba(238, 237, 233, 0.986); 
  }

  .openSans{
    font-family: 'Open Sans', sans-serif !important;
  }

  input { 
    text-align: center;
    padding-top:0.5rem;
    padding-bottom: 0.5rem; 
  }

  input, select, textarea{
    color: rgb(0, 0, 0);
    font-weight: 400;
  }
</style>
