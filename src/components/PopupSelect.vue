<template>
  <div class="popup">
    <input
      value="cont"
      id="cont"
      type="radio"
      v-model="tempData"
      class="radio"
    />
    <label for="cont"> Sitemap contains </label>
    <input
      value="notcont"
      id="notcont"
      type="radio"
      v-model="tempData"
      class="radio"
    />
    <label for="notcont">
      Sitemap doesn't contains
    </label>

    <input
      value="exact"
      id="exact"
      type="radio"
      v-model="tempData"
      class="radio"
    />
    <label for="exact">
      Exact match
    </label>
    <hr />
    <div class="buttons">
      <button class="red" @click="popupToggle">Reset</button>
      <button class="blue" @click="applyFilterChange">Apply</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["filterParametrs"],
  data: function() {
    return {
      tempData: this.filterParametrs
    };
  },
  methods: {
    popupToggle() {
      this.$emit("popupToggle");
    },
    applyFilterChange() {
      this.$emit("applyChange", this.tempData);
    }
  }
};
</script>

<style>
.popup {
  position: absolute;
  width: 275px;
  height: 180px;
  top: 144px;
  left: 20px;
  z-index: 100;
  background: #ffffff;
  border: 1px solid #bac9db;
  box-sizing: border-box;
  box-shadow: 0px 2px 8px rgba(162, 164, 169, 0.46);
  border-radius: 5px;
  display: flex;
  flex-direction: column;
  text-align: left;
}
label,
.radio {
  margin-top: 20px;
  margin-left: 23px;
}
.radio {
  position: absolute;
  z-index: -1;
  opacity: 0;
  margin: 10px 0 0 7px;
}
.radio + label {
  position: relative;
  padding: 0 0 0 35px;
  cursor: pointer;
}
.radio + label:before {
  content: "";
  position: absolute;
  top: -2px;
  left: 1px;
  width: 22px;
  height: 22px;
  border-radius: 50%;
  background: url("../Assets/icons/radiouncheced.svg") center no-repeat;
}
.radio + label:after {
  content: "";
  position: absolute;
  top: 1px;
  left: 4px;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: url("../Assets/icons/radiocheck.svg") center no-repeat;
  opacity: 0;
  transition: 0.2s;
}
.radio:checked + label:after {
  opacity: 1;
}
hr {
  width: 264px;
  margin-top: 19px;
  border-top: 1px solid #eaecef;
}
.buttons {
  width: 235px;
  display: flex;
  justify-content: space-between;
  margin-left: 18px;
  margin-top: 10px;
  box-sizing: border-box;
}
.buttons button {
  border: none;
  background: none;
  width: 36px;
  height: 16px;
  outline: 0;
  cursor: pointer;
}
.buttons .blue {
  font-weight: 500;
}
</style>
