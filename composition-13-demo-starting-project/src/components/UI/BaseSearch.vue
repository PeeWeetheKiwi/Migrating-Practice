<template>
  <form>
    <input type="search" @input="$emit('search', $event.target.value)" :value="searchTerm" placeholder="Filter items" />
  </form>
</template>

<script>
export default {
  props: ['searchTerm'],
  emits: ['search'],
};
</script>

<style scoped>
input {
  font: inherit;
  width: 100%;
  display: block;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus {
  outline: none;
  border-color: #00006b;
  background-color: #eeeeff;
}
</style>