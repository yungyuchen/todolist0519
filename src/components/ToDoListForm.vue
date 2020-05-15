<template>
  <div id="todolist-form">
    <!-- <form v-on:submit="todolistSubmit"> -->
    <!-- <form v-on:click="todolistSubmit"> -->
    <form @submit.prevent="todolistSubmit">
      <label>ToDoList</label>
      <input v-model="todolist.table" type="text" />
      <button>Add ToDoList</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'todolist-form',
    data() {
      return {
        todolist: {
          table: '',
        },
      }
    },
    methods: {
      todolistSubmit(){
        console.log('hihi')
        this.$emit('add:todolist', this.todolist)
      },
    },
  }
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }
</style>