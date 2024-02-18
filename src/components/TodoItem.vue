<template>
  <div>
    <li class="d-flex">
      <b class="me-3"> {{ data.id }} </b>
      <div v-if="!data.editing">
        <span>{{ data.title }}</span>
      </div>

      <div v-if="data.editing">
        <input
          type="text"
          v-model="editingTodoProps.title"
          class="form-control"
          @keyup.enter="save(data)"
        />
      </div>

      <button
        @click="edit(data.id)"
        class="btn btn-outline-primary btn-sm ms-3"
      >
        EDIT
      </button>

      <button
        @click="remove(data.id)"
        class="btn btn-outline-warning btn-sm ms-3"
      >
        DELETE
      </button>
    </li>
  </div>
</template>

<script>
export default {
  props: ["data", "editingTodoProps"],
  data() {
    return {};
  },
  methods: {
    remove(id) {
      this.$emit("removeEmit", id);
    },
    edit(id) {
      this.$emit("editEmit", id);
    },
    save(todo) {
      this.$emit("saveEmit", todo);
    },
  },
};
</script>

<style scoped>
li {
  list-style: none;
  margin-top: 10px;
}
</style>
