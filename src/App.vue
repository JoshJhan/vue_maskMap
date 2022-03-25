<template>
  <div id="app">
    <!-- 側攔區塊: -->
    <!-- 自定義事件 @triggerMarkerPopup -->
    <asideMenu @triggerMarkerPopup="openPopup" ref="menu" />
    
    <!-- 地圖區塊 -->
    <maskMap ref="map"/>
    <!-- 藥局資訊 -->
    <lightBox />
  </div>
</template>

<script>
import { mapActions } from "vuex";
import asideMenu from "./components/asideMenu";
import lightBox from "./components/lightBox";
import maskMap from "./components/maskMap";
export default {
  name: "App",
  components: { asideMenu, lightBox, maskMap },
  methods: {
    ...mapActions(["fetchLocations", "fetchPharmacies"]),
    openPopup(id){
      this.$refs.map.triggerPopup(id);
    }
  },
  mounted() {
    this.fetchLocations();
    this.fetchPharmacies();
  },
};
</script>

<style lang="scss" src="./style.scss"></style>
