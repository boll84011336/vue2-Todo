<template>
  <div id="todoList">
    <h1>Vue 2 TodoList</h1>
    <div class="d-flex">
      <input
        type="text"
        v-model="todo"
        class="form-control"
        @keyup.enter="addTask"
      />
      <button class="add btn btn-sm" @click="addTask">Add</button>
    </div>

    <div id="todos">
      <ul>
        <li v-for="item in todos" :key="item.id" class="d-flex">
          <b class="me-3"> {{ item.id }} </b>
          <div v-if="!item.editing">
            <span>{{ item.title }}</span>
          </div>

          <div v-if="item.editing">
            <input
              type="text"
              v-model="editingTodo.title"
              class="form-control"
              @keyup.enter="saveEdit(item)"
            />
          </div>

          <button
            @click="editTask(item.id)"
            class="btn btn-outline-primary btn-sm ms-3"
          >
            EDIT
          </button>

          <button
            @click="removeTask(item.id)"
            class="btn btn-outline-warning btn-sm ms-3"
          >
            DELETE
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todo: "",
      todos: [
        { id: 1, title: "睡覺", editing: false },
        { id: 2, title: "吃飯", editing: false },
      ],
      nextId: 3, //唯一ID
      editingTodo: "",
    };
  },
  methods: {
    addTask() {
      if (this.todo.trim() !== "") {
        this.todos.push({
          id: this.nextId,
          title: this.todo.trim(),
          editing: false,
        });
        this.todo = "";
        this.nextId++;
      }
    },
    removeTask(id) {
      const index = this.todos.findIndex((item) => item.id === id);
      console.log(index);
      if (index !== -1) {
        this.todos.splice(index, 1);
      }
    },
    editTask(id) {
      // 把狀態修改
      console.log(id);
      const todo = this.todos.find((item) => item.id === id);
      if (todo !== "") {
        this.editingTodo = { ...todo };
        todo.editing = !todo.editing;
      }
    },
    saveEdit(item) {
      // 保存編輯的資料
      item.title = this.editingTodo.title;
      item.editing = false;
      this.editingTodo = null;
    },
  },
};
</script>

<style scoped>
#todoList {
  margin: 0 auto;
  max-width: 350px;
}

h1 {
  color: rgb(43, 237, 237);
}

.add {
  margin-left: 10px;
  border: 3px solid lightblue;
  padding: 5px 15px;
  background-color: lightblue;
  color: black;
}

li {
  list-style: none;
  margin-top: 10px;
}
.todo {
  text-align: left;
  cursor: pointer;
}
.completed {
  text-decoration: line-through;
}
</style>
