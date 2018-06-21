<template>
  <div class="header">
    <h1>ComunicaWeb | TodoList</h1>

    <p>Total of tasks: {{ totalTasks }}</p>

    <hr>
  </div>
</template>

<script>
export default {
  props: ['totalTasks'],
}
</script>


<style lang="scss">
  .header {
    margin-bottom: 2rem;

    h1 {
      margin-bottom: 0;
    }
  }

</style>

