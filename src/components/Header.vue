<template>
  <div class="navbar">
    <md-content class="md-elevation-3">
      <div class="md-layout">
        <div class="md-layout-item">
          <div class="brand">
            <h1>COVID-19 NEWS</h1>
          </div>
        </div>
        <div class="md-layout-item">
          <md-field>
            <md-icon>search</md-icon>
            <label>Buscar</label>
            <md-input v-model="searchValue" @keyup="filterNews"></md-input>
          </md-field>
        </div>
        <div class="md-layout-item"></div>
      </div>
    </md-content>
  </div>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      searchValue: ""
    };
  },
  methods: {
    filterNews() {
      this.$emit("filterNews", this.searchValue);
    }
  }
};
</script>

<style>
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  color: #000000;
  z-index: 99;
}
.brand {
  display: flex;
  height: 100%;
  justify-content: center;
  align-items: center;
  font-size: 12px;
  line-height: 1;
  padding-left: 16px;
  padding-right: 16px;
}
</style>