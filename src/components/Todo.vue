<template>
  <div style="margin-top: 40px;" class="wrapper">
    <el-row type="flex" justify="center">
      <el-col :sm="16" :md="12">
        <el-card class="boxCard">
          <h2>Add New</h2>
          <el-input
            class="largeInput"
            v-model="todoInput"
            ref="refocus"
            placeholder="What's next?"
            autofocus
            @keyup.enter.native="addTodo">
          </el-input>
        </el-card>
        <el-collapse-transition>
          <el-card class="boxCard" v-if="todoList.length > 0">
            <el-table
              :data="todoList"
              style="width: 100%;"
              :show-header="false"
              :row-class-name="tableRowClass"
              size="mini">
              <el-table-column
                prop="done"
                label="✅"
                sortable
                width="50px"
                style="text-align: center;">
                <template slot-scope="scope">
                  <el-checkbox v-model="scope.row.done"></el-checkbox>
                </template>
              </el-table-column>
              <el-table-column
                prop="name"
                label="Todo Item">
              </el-table-column>
              <el-table-column
                label="Control"
                width="80px"
                style="text-align: center;">
                <template slot-scope="scope">
                  <el-button v-on:click="editTodoOpen(scope.row)" icon="el-icon-edit" type="text"></el-button>
                  <el-button v-on:click="deleteTodo(scope.row)" icon="el-icon-delete" type="text"></el-button>
                </template>
              </el-table-column>
            </el-table>
          </el-card>
        </el-collapse-transition>
        <el-dialog
          class="dialogBox"
          title="Edit Todo"
          :visible.sync="editBox">
          <el-input
            v-model="editTodo"
            autofocus>
          </el-input>
          <span slot="footer">
            <el-button @click="editTodoCancel">Cancel</el-button>
            <el-button type="primary" @click="editTodoSave">Confirm</el-button>
          </span>
        </el-dialog>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: 'Todo',

  data () {
    return {
      todoList: [],
      todoInput: '',
      editTodo: '',
      editBox: false
    }
  },

  methods: {
    addTodo () {
      if (this.todoInput !== '') {
        this.todoList.push({ name: this.todoInput, done: false })
        this.todoInput = ''
        this.todoSelectedList = null
        this.$refs.search.focus()
      }
    },
    deleteTodo (item) {
      var toDelete = this.todoList.indexOf(item)
      this.todoList.splice(toDelete, 1)
    },
    editTodoOpen (item) {
      this.editBox = true
      this.editTodoIndex = this.todoList.indexOf(item)
      this.editTodo = this.todoList[this.editTodoIndex].name
    },
    editTodoSave (item) {
      this.todoList[this.editTodoIndex].name = this.editTodo
      this.editTodo = ''
      this.editTodoIndex = null
      this.editBox = false
    },
    editTodoCancel () {
      this.editTodo = ''
      this.editTodoIndex = null
      this.editBox = false
    },
    checkInputEmpty () {
      return this.todoInput === ''
    },
    tableRowClass ({ row, rowIndex }) {
      if (row.done) {
        return 'itemDone'
      }
      return ''
    }
  }
}
</script>

<style>
  h2 {
    margin-top: 0px;
  }
  .el-table .itemDone {
    background: #f0f9eb;
  }
  .boxCard {
    margin-bottom: 20px;
  }
  .wrapper {
    min-height: 100vh;
  }
  .el-table--mini {
    font-size: 16px;
  }
  .el-dialog {
    width: 500px;
    max-width: 90%;
  }
</style>
