<template>
  <div class="d-flex">
    <input
      type="text"
      v-model="todo"
      class="form-control"
      @keyup.enter="addTask"
    />
    <button class="add btn btn-sm" @click="addTask">Add</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todo: "",
    };
  },
  methods: {
    addTask() {
      this.$emit("add", this.todo);
      this.todo = "";
    },
  },
};
</script>

<style scoped>
.add {
  margin-left: 10px;
  border: 3px solid lightblue;
  padding: 5px 15px;
  background-color: lightblue;
  color: black;
}
</style>
