<template>
  <div class="">
    <form @submit="addTodos">
      <div class="flex justify-center">
        <input type="text" name="title" v-model="title" placeholder="Add Task" class="shadow appearance-none border rounded openSans">
      </div>
      
      <div class=" my-3 flex justify-center rounded-lg shadow  bg-green-600">
        <input type="submit" value="SUBMIT"  class="cursor-pointer">
      </div>
      
        
    </form>
  </div>
</template>

<script>
  export default {
    name: "AddTodosItem",
    props: ['editItems'],
    data () {
      return {
        title: '',
        id: '',
        edit: false
      }
    },
    methods: {
      addTodos(e){
        e.preventDefault();
        if (this.edit === false){
          // add new task
          const newTodo = {
            title: this.title,
            id: Math.floor(Math.random() * 100)
          };
          if (newTodo.title !== ''){
            this.$emit('add-newToo-event', newTodo);
          }
          this.title = ''
        }else{
          //edit task
          const editItem = {
            title: this.title,
            id: this.id
          };
          //send to parent (App.vue)
          this.$emit('edit-item-event', editItem);
          // clear input field
          this.title = '';
          this.edit = false;
        }
      }
    },
    watch: {
      editItems: {
        handler() {
          this.title = this.editItems.title;
          this.id = this.editItems.id;
          this.edit = true
        },
        deep: true
      },
      title:{
        handler(){
          if(this.title === ''){
              this.edit = false;
          }
        }
      }
    }
  }
</script>

<style scoped>

</style>
