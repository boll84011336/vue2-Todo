<template>
  <div>
    <button @click="handleClick" :class="buttonClass">
      {{ buttonText }}
    </button>
  </div>
</template>

<script>
export default {
  props: {
    buttonClass: String,
    buttonText: String,
    handleClick: Function,
  },
  data() {
    return {};
  },
};
</script>

<style></style>
