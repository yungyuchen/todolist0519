<template>
  <div id="todolist-table">
    <p v-if="todolists.length < 1" class="empty-table">
      No ToDoList
    </p>
    <table v-else>
      <thead>
        <tr>
          <th>ToDoList</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="todolist in todolists" :key="todolist.id">
          <td v-if="editing === todolist.id">
            <input type="text" v-model="todolist.table" />
          </td>
          <td v-else>{{ todolist.table }}</td>
          <td v-if="editing === todolist.id">
            <button @click="editTodolists(todolist)">Save</button>
            <button class="muted-button" @click="editing = null">Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(todolist.id)">Edit</button>
            <button @click="$emit('delete:todolist', todolist.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'todolist-table',
    props: {
      todolists: Array,
    },
    data(){
      return{
        editing:null,
      }
    },
    methods:{
      editMode(id){
        this.editing =id
      },

      editTodolists(todolist){
        if(todolist.table ==='') return
        this.$emit('edit:todolist' ,todolist.id, todolist)
        this.editing = null
      }
    }
  }
</script>

<style scoped>
 button {
    margin: 0 0.5rem 0 0;
    float: right;
  }
</style>