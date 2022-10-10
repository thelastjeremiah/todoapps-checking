<template>
  <div>
    <h2 class="openSans text-center uppercase py-5">Todo App</h2>
    <div v-bind:key="tododata.id" v-for="tododata in todoData">
      <TodoItem v-bind:tododata="tododata" v-on:del-todo-item="delTodoMethod" v-on:edit-todo-item="editTodoMethod"/>
    </div>
    <div v-if="!todoData.length">
      <p class="openSans text-center py-2 uppercase ">No List Of Todos</p>
    </div>
  </div>
</template>

<script>
  import TodoItem from "./TodoItem";
  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: "Todos",
    props: ["todoData"],
    components: {
      TodoItem
    },
    methods: {
      delTodoMethod(id){
        //send to parent
        this.$emit('del-todo-events', id);
      },
      editTodoMethod(id){
        //send to parent (App.vue)
        this.$emit('edit-Todo-event', id)
      }
    }
  }

</script>

<style scoped>
  .flex{
    display:flex;
    justify-content: center;
    align-content: center;
  }

  .padding-id{
    padding-top:0.4rem;
    padding-right:1rem;
  }
</style>
