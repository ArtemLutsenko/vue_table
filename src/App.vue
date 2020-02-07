<template>
  <div class="container">
    <div class="wrapper">
      <app-table></app-table>
    </div>
  </div>
</template>

<script>
import Table from "./components/Table";

export default {
  components: {
    appTable: Table
  }
};
</script>

<style>
.container {
  width: 100%;
  height: 93vh;
}
.wrapper {
  margin: 50px auto 0;
  width: 920px;
}
</style>
