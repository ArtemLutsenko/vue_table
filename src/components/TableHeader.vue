<template>
  <div class="table-row table-header">
    <div class="checkbox-container" @click="selectAllSitemaps">
      <div class="checkbox" :class="{ checked: allChecked }"></div>
    </div>
    <div class="sitemap">
      <p>Sitemap ({{ numberOfRows }})</p>
    </div>
    <div class="sitemap-index">Type</div>
    <div class="date">Submited</div>
    <div class="date">Last check</div>
    <div class="status">Status</div>
    <div class="urls">URLs</div>
    <div class="recrewl">Recrewl sitemap</div>
    <div class="delete">Remove sitemap</div>
  </div>
</template>

<script>
export default {
  props: ["numberOfRows", "allChecked"],
  data: function() {
    return {
      // checkboxStatus: this.allChecked
    };
  },
  methods: {
    selectAllSitemaps() {
      //  this.checkboxStatus = !this.checkboxStatus
      this.$emit("selectAllSitemaps", this.allChecked);
    }
  }
};
</script>

<style>
.table-header {
  background: #f6f8fe;
  border-top: 1px solid #c2cfe0;
  box-sizing: border-box;
  border-radius: 0px;
  font-weight: bold;
}
</style>
