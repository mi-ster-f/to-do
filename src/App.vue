<template>
  <b-container>
    <b-row>
      <div class="row1"></div>
    </b-row>
    <b-row class="row2">
      <b-col class="col2" cols="8">
        <h1>My to-do list</h1>
        <b-form-input
          v-model="currentTodo"
          @keydown.enter="addTodo()"
          placeholder="Add a to-do"
          class="formInput md-title"
        ></b-form-input>
        <md-list class="todos ">
          <md-list-item
            v-for="todo in todos"
            :key="todo.id"
            @dblclick="setToEdited(todo)"
            :class="{ editing: todo == editedToDoId }"
            class="listItem"
          >
            <input
              v-model="todo.completed"
              type="checkbox"
              class="checkboxStyles"
            />
            <span
              v-show="editedToDoId !== todo.id"
              :class="{ taskComplete: todo.completed }"
              class="md-display-3"
              >{{ todo.label }}
              <md-tooltip class="toolTip" md-direction="left"
                >Double click to edit</md-tooltip
              >
            </span>
            <input
              v-model="todo.label"
              v-show="editedToDoId == todo.id"
              v-on:keyup.enter="updateTodo()"
              class="editFormInput md-display-1"
            />
            <button @click="removeTodo(todo)" class="buttonStyles">
              Delete
            </button>
          </md-list-item>
        </md-list>
      </b-col>
    </b-row>
    <b-row>
      <div class="row3"></div>
    </b-row>
  </b-container>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: '',
      editedToDoId: null,
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
      });
      this.currentTodo = '';
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    setToEdited(todo) {
      this.editedToDoId = todo.id;
    },
    updateTodo() {
      this.editedToDoId = null;
    },
  },
};
</script>

<style>
body {
  text-align: center;
  background-color: black;
  margin: 0 auto;
  font-size: 20px;
}

h1 {
  margin-top: 50px;
  margin-bottom: 50px;
  font-size: 56px;
  font-family: 'Dancing Script', cursive;
}

.row1 {
  height: 15%;
}

.row3 {
  height: 15%;
}

.col2 {
  background-color: #f9e79f;
  display: inline-block;
  width: 80%;
  min-height: 600px;
  box-shadow: 5px 10px white;
  font-family: 'Permanent Marker', cursive;
  font-size: 1rem;
}

.toolTip {
  color: blue;
}

.editing {
  display: none;
}
.taskComplete {
  text-decoration: line-through;
  opacity: 0.5;
}

.todos {
  margin-top: 100px;
}

.listItem {
  margin-top: 10px;
  word-wrap: break-word;
  border-bottom: 0.5px dotted white;
  margin-bottom: 10px;
}

.formInput {
  text-decoration: none;
  border: none;
  box-shadow: 2px 3px black;
  opacity: 50%;
  text-align: center;
  margin-bottom: 20px;
}

.editFormInput {
  opacity: 40%;
  border: none;
  width: 40%;
  text-align: center;
  line-height: 18px;
}

.checkboxStyles {
  float: left;
}

.buttonStyles {
  float: right;
  border-radius: 6px;
  color: white;
  background-color: darkgoldenrod;
  border-left: 10px;
}

/* Responsive layouts */

@media screen and (max-width: 767px) {
  .col2 ul {
    width: 80%;
  }
  body h1 {
    font-size: 76px;
  }
}
</style>
