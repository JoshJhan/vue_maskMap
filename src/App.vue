<template>
  <div id="app">
    <!-- 側攔區塊 -->
    <asideMenu />

    <!-- 地圖區塊 -->
    <div class="mask-map" id="mask-map"></div>
  </div>
</template>

<script>
import { mapActions } from "vuex";
import asideMenu from "./components/asideMenu";
export default {
  name: "App",
  components: { asideMenu },
  methods: {
    ...mapActions(["fetchLocations", "fetchPharmacies"]),
  },
  mounted() {
    this.fetchLocations();
    this.fetchPharmacies();
  },
};
</script>

<style lang="scss" src="./style.scss"></style>
