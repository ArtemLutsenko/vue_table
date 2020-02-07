<template>
  <div class="filters">
    <p>Filters:</p>
    <div class="input-filters">
      <input
        type="text"
        placeholder="URL or its part"
        class="filter-input"
        v-model="urlSerch"
        @click="popupToggle"
      />
      <div class="select">
        <select name="Types" id="types" disabled class="filter-select">
          <option value="all">All types</option>
        </select>
      </div>
      <div class="select">
        <select name="submited" id="sub" disabled class="filter-select">
          <option value="submitted">Submitted</option>
        </select>
      </div>
      <div class="select date-select">
        <select name="interval" id="interval" disabled class="filter-select">
          <option value="interval">2/12/19 - 2/12..</option>
        </select>
      </div>
      <div class="select">
        <select
          name="status"
          id="status"
          class="filter-select sitemap-select"
          v-model="typeSearch"
        >
          <option value="all">All sitemaps</option>
          <option value="suc">Success</option>
          <option value="not_f">Couldn't fetch</option>
          <option value="err">Errors</option>
        </select>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      urlSerch: "",
      typeSearch: "all"
    };
  },
  methods: {
    popupToggle() {
      this.$emit("popupToggle");
    }
  },
  watch: {
    urlSerch() {
      this.$emit("setFilterParametrs", this.urlSerch, this.typeSearch);
    },
    typeSearch() {
      this.$emit("setFilterParametrs", this.urlSerch, this.typeSearch);
    }
  }
};
</script>

<style>
.filters {
  background-color: #eaedf5;
  border-top: 1px solid #c2cfe0;
  box-sizing: border-box;
  border-radius: 0px;
}
.filters p {
  font-weight: 500;
  text-align: left;
  margin-left: 23px;
  display: block;
  margin-bottom: 5px;
  margin-top: 13px;
}
.input-filters {
  display: flex;
  padding-bottom: 11px;
}
.filter-input,
.filter-select {
  height: 30px;
  width: 162px;
  background: #ffffff;
  border: 1px solid #c2cfe0;
  box-sizing: border-box;
  border-radius: 5px;
  padding-left: 12px;
  box-sizing: border-box;
  -webkit-appearance: none;
  -moz-appearance: none;
  -ms-appearance: none;
  appearance: none;
  outline: 0;
  box-shadow: none;
  cursor: pointer;
  color: #34495d;
}
.filter-input {
  margin-left: 21px;
}
.filter-select {
  margin-left: 16px;
}
.filter-input::placeholder {
  color: #a5b5cb;
}
.filter-select::-ms-expand {
  display: none;
}

.select {
  position: relative;
  display: flex;
}
/* Arrow */
.select::after {
  content: " ";
  position: absolute;
  width: 30px;
  height: 30px;
  top: 0;
  right: 0;
  padding: 0 1em;
  border-left: 1px solid #c2cfe0;
  background-image: url("../Assets/icons/downErrow.svg");
  background-repeat: no-repeat;
  background-position: center;
  cursor: pointer;
  pointer-events: none;
  box-sizing: border-box;
}
.date-select::before {
  content: " ";
  position: absolute;
  width: 30px;
  height: 30px;
  top: 0;
  left: 18px;
  padding: 0 1em;
  background-image: url("../Assets/icons/calendar.svg");
  background-repeat: no-repeat;
  background-position: center;
  cursor: pointer;
  pointer-events: none;
  box-sizing: border-box;
}
.date-select select {
  padding-left: 30px;
}
.sitemap-select option {
  margin-top: 15px;
  font-size: 14px;
  line-height: 16px;
  letter-spacing: 0.01em;
  color: #34495d;
}
</style>
