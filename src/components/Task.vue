<template>
  <li
    :class="{'done' : task.done}"
    @click="doneTask"
  >
    <span class="text">{{ task.name }}</span>
    <span class="link" @click="removeTask">remove</span>
  </li>
</template>

<script>
export default {
  props: ['task'],

  methods: {
    doneTask() {
      this.$emit('doneTask', this.task.id);
    },

    removeTask() {
      this.$emit('removeTask', this.task.id);
    }
  },
}
</script>

<style lang="scss">
  li {
    padding: 1rem;
    background-color: #ffffff;
    border-bottom: 1px solid #cccccc;

    display: flex;
    justify-content: space-between;

    &:last-child {
      border-bottom-color: transparent;
    }

    &:hover {
      background-color: darken(#ffffff, 5%);
      cursor: pointer;
    }

    &.done > .text {
      text-decoration: line-through;
      color: #999999;
    }

    .link {
      color: blue;

      &:hover {
        text-decoration: underline;
      }
    }
  }
</style>


