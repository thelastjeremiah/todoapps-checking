<template>

  <div class="flex  pt-5">
    <div class="border-black openSans pt-2 px-3">
      {{tododata.title}}
    </div>

    <div class="px-8">
      <p class="pb-3 openSans">Edit</p>
      <i class="fa-solid fa-pen-to-square cursor-pointer" @click="$emit('edit-todo-item', tododata.id)"></i>
    </div>
    
    <div>
      <p class="pb-3 openSans">Delete</p>
      <i class="fa-solid fa-eraser cursor-pointer" @click="$emit('del-todo-item', tododata.id)"></i>
    </div>
  
  </div>


</template>

<script>
    export default {
        name: "TodoItem",
        props: ["tododata"]
    }

</script>

<style scoped>
  .glyphicon-pencil, .glyphicon-trash{
    font-size: 15px;
    padding: 4px;
  }


</style>
