<template>
  <div id="todolist-form">
    <!-- <form v-on:submit="todolistSubmit"> -->
    <!-- <form v-on:click="todolistSubmit"> -->
    <form @submit.prevent="todolistSubmit"><!-- 呼叫這個todolistSubmit事件 -->
      <label>ToDoList</label>
      <input v-model="todolist.table" type="text" /><!-- 雙向帶值 -->
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
      todolistSubmit(){ //事件監聽方法
        this.$emit('add:todolist', this.todolist) // 傳遞值給父主件，App.vue創建一個名為的事件add:todolist，然後通過this.todolist
      },
    },
  }
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }
</style>