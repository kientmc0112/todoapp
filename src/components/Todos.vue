<template>
  <div class="row todo-content">
    <div class="col-md-6">
      <div class="todo-list not-done">
        <h1>TODOS</h1>
        <div class="input-group mb-3">
          <input type="text" class="form-control" placeholder="Enter content" v-model="textContent">
          <div class="input-group-append">
            <button class="btn btn-outline-secondary" type="button" id="button-addon2" @click="addTask()">Add</button>
          </div>
        </div>
        <hr>
        <ul class="list-unstyled" v-for="(todo, index) in todos" :key="todo.id">
          <li class="ui-state-default li-items mt-1">
            <div class="input-group">
              <div class="input-group-prepend">
                <div class="input-group-text">
                  <input type="checkbox" v-model="todo.checked" aria-label="Radio button for following text input">
                </div>
              </div>
              <input type="text" class="form-control" :class="{ 'done-task': todo.completed }" v-model="todo.content">
              <div class="input-group-append remove-icon">
                <span class="input-group-text" @click="deleteTask(index)">&#10060;</span>
              </div>
            </div>
          </li>
        </ul>
        <hr>
        <div class="todo-footer row">
          <div class="col-md-6">
            <div class="form-check form-check-inline" @click="checkAll(true)">
              &#9989;
              <label class="form-check-label" for="inlineRadio1">Check all</label>
            </div>
            <div class="form-check form-check-inline" @click="checkAll(false)">
              &#10062;
              <label class="form-check-label" for="inlineRadio2">UnCheck all</label>
            </div>
          </div>
          <div class="col-md-6 save-all">
            <div class="form-check form-check-inline save-all">
              <button type="button" class="btn btn-success btn-sm" @click="doneAll()">DONE ALL &#10004;</button>
            </div>
            <div class="form-check form-check-inline save-all">
              <button type="button" class="btn btn-dark btn-sm" @click="deleteAll()">DEL ALL &#10006;</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Todos',
  data: function () {
    return {
      todos: [
        {
          'id': 1,
          'content': 'Noi dung 1',
          'checked': false,
          'completed': false
        },
        {
          'id': 2,
          'content': 'Noi dung 2',
          'checked': true,
          'completed': true
        }
      ],
      textContent: '',
      idCurrent: 2
    }
  },
  methods: {
    addTask () {
      if (this.textContent.trim().length > 0) {
        this.idCurrent++
        this.todos.push({
          'id': this.idCurrent,
          'content': this.textContent,
          'checked': false,
          'completed': false
        })
        this.textContent = ''
      }
    },
    deleteTask (index) {
      this.todos.splice(index, 1)
    },
    checkAll (flag) {
      this.todos.forEach(todo => {
        todo.checked = flag
      })
    },
    doneAll () {
      this.todos.filter(function (item) {
        if (item.checked) {
          item.completed = true
        }
      })
    },
    deleteAll () {
      this.todos = this.todos.filter(function (item) {
        return !item.checked
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .todo-content {
    display: flex;
    justify-content: center;
  }

  .todo-list h1 {
    margin-top: 20px;
    padding-bottom: 20px;
    text-align: center;
    font-weight: bold;
  }

  .todo-footer {
    background-color: #d2e8ca;
    padding: 10px 20px 15px;
  }

  #done-items li {
    padding: 10px 0;
    border-bottom: 1px solid #ddd;
    text-decoration: line-through;
  }

  .done-task {
    text-decoration: line-through;
    color: orange;
  }

  .form-check-inline {
    cursor: pointer;
  }

  .remove-icon span {
    cursor: pointer;
  }

  .save-all {
    float: right;
  }
</style>
