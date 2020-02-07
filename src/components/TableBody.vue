<template>
  <div class="table-row" :class="{ lightblue: siteInfo.checked }">
    <div class="checkbox-container" @click="selectItem(siteInfo.id)">
      <div class="checkbox" :class="{ checked: siteInfo.checked }"></div>
    </div>
    <div class="sitemap">
      <a :href="siteInfo.path">/{{ getSitemap }}</a>
    </div>
    <div class="sitemap-index">Sitemap index</div>
    <div class="date">{{ getSubmitDate }}</div>
    <div class="date">{{ getLastCheckDate }}</div>
    <div class="status" :class="getStatus == 'Success' ? 'green' : 'red'">
      {{ getStatus }}
    </div>
    <div class="urls">{{ getFormatedUrls }}</div>
    <div class="recrewl">
      <button class="table-row-btn" :class="{ lightblue: siteInfo.checked }">
        Recrewl
      </button>
    </div>
    <div
      title="Remove from Search Console"
      class="delete"
      @click="deleteItem(siteInfo.id)"
    >
      <appDeletesvg class="delete-icon"></appDeletesvg>
    </div>
  </div>
</template>

<script>
import DeleteSvg from "../Assets/icons/DeleteSvg";
export default {
  props: ["siteInfo"],
  components: {
    appDeletesvg: DeleteSvg
  },
  methods: {
    formatedData(date) {
      let tdate = new Date(date);
      const day = tdate.getDate();
      const month = tdate.toLocaleString("default", { month: "short" });
      const year = tdate.getFullYear();
      return `${month} ${day}, \n ${year}`;
    },
    deleteItem(index) {
      this.$emit("deleteItem", index);
    },
    selectItem() {
      this.$emit("selectSitemap", this.siteInfo.id);
    }
  },
  computed: {
    getSitemap: function() {
      return this.siteInfo.path.match(/\/([^/]+)\/?$/)[1];
    },
    getCheckboxValue: function() {
      return this.siteInfo.checked;
    },
    getLastCheckDate: function() {
      return this.formatedData(this.siteInfo.lastCheck);
    },
    getSubmitDate: function() {
      return this.formatedData(this.siteInfo.lastSubmitted);
    },
    getStatus: function() {
      if (this.siteInfo.errors === 0) {
        return "Success";
      } else if (this.siteInfo.errors === 1) return "1 error";
      else return this.siteInfo.errors + " errors";
    },
    getFormatedUrls: function() {
      return new Intl.NumberFormat().format(this.siteInfo.urls);
    },
    getFake: function() {
      return new Intl.NumberFormat().format(this.siteInfo.fake);
    }
  }
};
</script>

<style>
.table-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
  width: 918px;
  height: 70px;
  border-radius: 0px 0px 0px 0px;
  margin: 0 auto;
  border-top: 1px solid #f2f4fb;
}
.checkbox-container {
  display: flex;
  justify-content: center;
  width: 20px;
  height: 20px;
  margin-left: 25px;
}
.checkbox {
  position: absolute;
  border: #c2cfe0 solid 2px;
  width: 18px;
  height: 18px;
  border-radius: 2px;
}
.checked {
  background-image: url("../Assets/icons/selected.svg");
  border: #0288d1 solid 2px;
  box-sizing: border-box;
  background-attachment: inherit;
  background-position: center;
}
.sitemap {
  position: relative;
  width: 130px;
  text-align: left;
}
.sitemap a {
  position: relative;
  text-decoration: none;
  color: #0288d1;
}
.sitemap a:after {
  display: block;
  position: absolute;
  top: 2px;
  right: -23px;
  content: " ";
  background-image: url("../Assets/icons/sitemap.svg");
  background-size: 13.5px 13.5px;
  height: 13.5px;
  width: 13.5px;
}
.sitemap-index {
  width: 74px;
}
.date {
  width: 75px;
  white-space: pre-line;
}
.status {
  width: 95px;
}
.urls {
  width: 85px;
}
.recrewl {
  width: 75px;
}
.table-row-btn {
  width: 72px;
  height: 25px;
  border: 1px solid #0288d1;
  box-sizing: border-box;
  border-radius: 4px;
  background-color: white;
  outline: 0;
  padding-top: 2px;
  color: #0288d1;
  cursor: pointer;
}
.table-row-btn:hover {
  background: #d2efff;
}
.delete-icon {
  fill: #9fa2b4;
}
.delete-icon:hover {
  fill: #fb6868;
  cursor: pointer;
}
.delete[title]:hover:after {
  content: attr(title);
  position: absolute;
  width: 204px;
  height: 32px;
  left: 680px;
  top: 49px;
  z-index: 30;
  background: #37474f;
  box-shadow: 0px 2px 6px rgba(0, 0, 0, 0.18);
  border-radius: 5px;
  color: #fafafa;
  padding-top: 8px;
  padding-left: 10px;
  box-sizing: border-box;
}
.delete {
  margin-right: 25px;
  width: 70px;
}
.lightblue {
  background-color: #e7f6ff;
}
</style>
