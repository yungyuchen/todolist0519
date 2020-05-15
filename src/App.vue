<template>
  <div id="app" class="small-container">
    <h1>ToDoList</h1>

	<todolist-form @add:todolist="addTodolists" />
    <todolist-table v-bind:todolists="todolists" @delete:todolist="deleteTodolists" @edit:todolist="editTodolists" />
  </div>
</template>

<script>
  import TodolistTable from '@/components/ToDoListTable.vue'
  import TodolistForm from '@/components/ToDoListForm.vue'

  export default {
    name: 'app',
    components: {
		TodolistTable,
		TodolistForm,
	},
	data(){
		return{
			todolists:[
				{
					id: 1,
					table:'熟悉Git指令',
				},
				{
					id: 2,
					table:'安裝Vue建置環境',
				},
				{
					id: 3,
					table:'整理技術筆記',
				},
			]
		}
	},
	methods: {
		addTodolists(todolist) {
			const lastId =
			this.todolists.length > 0
			? this.todolists[this.todolists.length - 1].id
			: 0;
			const id = lastId + 1;
			const newTodolist = { ...todolist, id };

			this.todolists = [...this.todolists, newTodolist];
		},
		deleteTodolists(id) {
			this.todolists = this.todolists.filter(
				todolist => todolist.id !== id
			)
		},
		editTodolists(id,updatedTodolist){
			this.todolists = this.todolists.map(
				todolist => todolist.id === id ? updatedTodolist : todolist
			)
		}
	}
	
  }
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>