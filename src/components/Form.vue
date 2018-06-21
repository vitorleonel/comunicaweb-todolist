<template>
  <form method="post" @submit.stop.prevent="addTask">
    <input type="text" name="task" v-model="task">
    <button type="submit">Add</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      task: '',
    }
  },

  methods: {
    addTask() {
      if(!this.task) {
        return;
      }

      this.$emit('addTask', this.task);
      this.task = '';
    }
  },
}
</script>


<style lang="scss">
  form {
    display: flex;

    input {
      height: 42px;
      padding: 0.5rem;
      margin-right: 1rem;
      border-width: 1px;
      flex: 1;

      &.error {
        border-color: #FF0000;
      }
    }

    button {
      width: 100px;
    }

  }
</style>

