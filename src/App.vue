<template>
  <div id="app" class="small-container">
    <h1>ToDoList</h1>

    <div style="display: black;">
      <form @submit.prevent="todolistSubmit" >
        <label>ToDoList</label>
        <input v-model="todolists.table" type="text" />
        <button @click="addTodolists">Add ToDoList</button>
      </form>
    </div>
    <div style="display: black;">
      <p style="display: none;">No ToDoList</p>
      <table>
        <thead>
          <tr>
            <th>ToDoList</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td style="display: none;">
              <input type="text" />
            </td>
            <td>熟悉Git指令</td>
            <td style="display: none;">
              <button>Save</button>
              <button>Cancel</button>
            </td>
            <td>
              <button>Edit</button>
              <button>Delete</button>
            </td>
          </tr>
          <tr>
            <td style="display: none;">
              <input type="text" />
            </td>
            <td>安裝Vue建置環境</td>
            <td style="display: none;">
              <button>Save</button>
              <button>Cancel</button>
            </td>
            <td>
              <button>Edit</button>
              <button>Delete</button>
            </td>
          </tr>
          <tr>
            <td style="display: none;">
              <input type="text" />
            </td>
            <td>整理技術筆記</td>
            <td style="display: none;">
              <button>Save</button>
              <button>Cancel</button>
            </td>
            <td>
              <button>Edit</button>
              <button>Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <br />
    <br />
    <br />

    <h1>ToDoList</h1>
    <todolist-form v-on:add:todolist="addTodolists" />
    <todolist-table
      v-bind:todolists="todolists"
      @delete:todolist="deleteTodolists"
      v-on:edit:todolist="editTodolists"
    />
  </div>
</template>

<script>
import TodolistTable from "@/components/ToDoListTable.vue";
import TodolistForm from "@/components/ToDoListForm.vue";

export default {
  name: "app",
  components: {
    TodolistTable,
    TodolistForm
  },
  data() {
    return {
      todolist: {
          table: '123',
        },
      todolists: [
        {
          id: 1, // 0
          table: "熟悉Git指令"
        },
        {
          id: 2, // 1
          table: "安裝Vue建置環境"
        },
        {
          id: 3, // 2
          table: "整理技術筆記"
        }
      ],

      
    };
  },
  methods: {
    todolistSubmit() {
      console.log('todolistSubmit')
      this.todolist = ("add:todolist", this.todolist);
      console.log(this.todolist);
    },

    addTodolists(todolist) {
      console.log('addTodolists')
      const lastId = this.todolists.length > 0 ? this.todolists[this.todolists.length - 1].id : 0; // 假如todolists長度大於1 取得最後一個ID
      // const lastId = this.todolists.length > 0 ? this.todolists.length : 0; // 假如todolists長度大於1 取得最後一個ID
      const id = lastId + 1; // 4
      const table = this.table;
      const newTodolist = { ...todolist, id , table }; //...todolist字串 ,

      this.todolists = [...this.todolists, newTodolist];
    },

    deleteTodolists(id) {
      this.todolists = this.todolists.filter(todolist => todolist.id !== id); // 直接顯示不等於點擊ID的每個項目,挑選不為ID的顯示
    },
    editTodolists(id, updatedTodolist) {
      this.todolists = this.todolists.map(todolist => todolist.id === id ? updatedTodolist : todolist
      );
    }
  }
};
</script>

<style>
form {
  margin-bottom: 2rem;
}

button {
  margin: 0 0.5rem 0 0;
  float: right;
}
button {
  background: #009435;
  border: 1px solid #009435;
}

.small-container {
  max-width: 680px;
}
</style>