<template>
  <div>
    <el-row type="flex" justify="center">
      <el-col :sm="16" :md="12">
        <el-card class="boxCard">
          <el-input v-model="todoInput" placeholder="What's next?">
            <template slot="append">
              <el-button :disabled="checkInputEmpty()" v-on:click="addTodo">Add</el-button>
            </template>
          </el-input>
        </el-card>
        <el-card class="boxCard" v-if="todoList.length > 0">
          <el-table
            :data="todoList"
            style="width: 100%;"
            :show-header="false"
            :row-class-name="tableRowClass">
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
              width="60px"
              style="text-align: center;">
              <template slot-scope="scope">
                <el-button v-on:click="deleteTodo(scope.row)" type="text" size="small">Delete</el-button>
              </template>
            </el-table-column>
          </el-table>
        </el-card>
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
      todoDue: ''
    }
  },

  methods: {
    addTodo () {
      if (this.todoInput !== '') {
        this.todoList.push({ name: this.todoInput, done: false })
        this.todoInput = ''
      }
    },
    deleteTodo (item) {
      var toDelete = this.todoList.indexOf(item)
      this.todoList.splice(toDelete, 1)
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
  .el-table .itemDone {
    background: #f0f9eb;
  }
  .boxCard {
    margin-bottom: 20px;
  }
</style>
