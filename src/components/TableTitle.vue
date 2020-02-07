<template>
  <div class="table-title">
    <div>
      <h2 class="table-title-header">Submited sitemaps</h2>
    </div>
    <div class="table-title-right">
      <p class="right-item" :class="{ hiden: !chekedCount }">
        Selected sitemaps: <span>{{ chekedCount }}</span>
      </p>
      <p class="lightgrey right-item" :class="{ blue: chekedCount }">
        Recrawl sitemaps
      </p>
      <p
        class="lightgrey right-item"
        :class="{ red: chekedCount }"
        @click="deleteSelectedSitemaps"
      >
        Remove sitemap
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["chekedCount"],
  methods: {
    deleteSelectedSitemaps() {
      this.$emit("deleteSelectedSitemaps");
    }
  }
};
</script>

<style>
.hiden {
  display: none;
}
.table-title {
  margin-top: 22px;
  display: flex;
  justify-content: space-between;
  margin-left: 24px;
}
.table-title-header {
  font-weight: bold;
  font-size: 20px;
  line-height: 23px;
  position: relative;
}
.table-title-header::after {
  display: block;
  position: absolute;
  top: 3px;
  right: -23px;
  content: " ";
  background-image: url("../Assets/icons/infoCircle.svg");
  background-size: 16px 16px;
  height: 16px;
  width: 16px;
  cursor: pointer;
}
.table-title-right {
  display: flex;
  justify-content: space-between;
}
.lightgrey {
  color: #c2cfe0;
  cursor: pointer;
}
.right-item {
  margin-right: 29px;
  margin-top: 17px;
}
.right-item span {
  font-weight: 600;
}
</style>
