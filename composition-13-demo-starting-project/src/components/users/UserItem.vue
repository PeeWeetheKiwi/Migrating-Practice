<template>
  <li>
    <h3>{{ userName }}</h3>
    <button @click="viewProjects">View Projects</button>
  </li>
</template>

<script>

export default {
  props: ['id', 'userName'],
  emits: ['list-projects'],
  setup(props) {
    function viewProjects() {
      this.$emit('list-projects', props.id);
    }
    return {
      viewProjects
    }
  }
}
//   methods: {
//     viewProjects() {
//       this.$emit('list-projects', props.id);
//     },
//   },
// };
</script>

<style scoped>
li {
  margin: 0.5rem 0;
  padding: 1rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.26);
  border: 1px solid #ccc;
}

li h3 {
  margin: 0;
}
</style>