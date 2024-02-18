<template>
  <div id="todoList">
    <h1>Vue 2 TodoList</h1>

    <InputTodo @add="addTask" />

    <div id="todos">
      <ul>
        <TodoItem
          v-for="todo in todos"
          :key="todo.id"
          :data="todo"
          @removeEmit="removeTask"
          @editEmit="editTask"
          @saveEmit="saveEdit"
          :editingTodoProps="editingTodo"
        />
      </ul>
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
import InputTodo from "./InputTodo.vue";

export default {
  components: { TodoItem, InputTodo },
  data() {
    return {
      todos: [
        { id: 1, title: "睡覺", editing: false },
        { id: 2, title: "吃飯", editing: false },
      ],
      nextId: 3, //唯一ID
      editingTodo: "",
    };
  },
  methods: {
    addTask(todo) {
      if (todo.trim() !== "") {
        this.todos.push({
          id: this.nextId,
          title: todo.trim(),
          editing: false,
        });
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
      if (todo) {
        this.editingTodo = { ...todo }; //這邊拿todo資料給editingTodo 傳進去TodoItem
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

.todo {
  text-align: left;
  cursor: pointer;
}
.completed {
  text-decoration: line-through;
}
</style>
