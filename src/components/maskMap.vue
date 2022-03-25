<template>
  <div class="mask-map" id="mask-map"></div>
</template>
<script>
import L from "leaflet";
export default {
  name: "maskMap",
  data() {
    return {
      // 因為別的地方用不到map 所以不需要丟到 vuex
      map: {},
      markers: [],
    };
  },
  computed: {
    currDistrictInfo() {
      return this.$store.getters.currDistrictInfo;
    },
    filteredStores() {
      return this.$store.getters.filteredStores;
    },
  },
  watch: {
    // 切換行政區
    currDistrictInfo(dist) {
      // this.map.panTo() 可以指定地圖中心點
      this.map.panTo(new L.LatLng(dist.latitude, dist.longitude));
    },
    filteredStores(stores) {
      // 先清除原有layer
      this.clearMarkers();

      // 根據藥局資訊加上對應 marker
      stores.forEach((element) => this.addMarker(element));
    },
  },
  methods: {
    addMarker(item) {
      // 標記圖示，可自行替換參數
      const ICON = {
        iconUrl:
          "https://raw.githubusercontent.com/pointhi/leaflet-color-markets/master/img/marker-icon-2x-violet.png",
        shadowUrl:
          "https://cdnjs.cloudflare.com/ajax/libs/leaflet/0.7.7/images/marker-shadow.png",
        iconSize: [25, 41],
        iconAnchor: [12, 41],
        popupAnchor: [1, -34],
        shadowSize: [41, 41],
      };

      // 將標記放置到地圖上
      const marker = L.marker([item.longitude, item.latitude], ICON)
        .addTo(this.map)
        .bindPopup(`<h2 class="popup-name">${item.name}</h2>`);

      // 替marker加入id與經緯度資訊
      marker.markerId = item.id;
      marker.lng = item.longitude;
      marker.lat = item.latitude;

      //   將marker push到陣列裡
      this.markers.push(marker);
    },
    clearMarkers() {
      // 清除地圖所有標記
      this.map.eachLayer((layer) => {
        if (layer instanceof L.Marker) {
          this.map.removeLayer(layer);
        }
      });

      // 加上清空陣列
      this.markers.length = 0;
    },
    triggerPopup(markerId) {
      // 找出目標標記
      const marker = this.markers.find((d) => d.markerId === markerId);

      //   將地圖中心指向目標標記，並開啟Popup
      this.map.flyTo(new L.LatLng(marker.lng, marker.lat), 15);
      marker.openPopup();
    },
  },
  mounted() {
    // 以下動作會將地圖初始化
    this.map = L.map("mask-map", {
      center: [25.03, 121.55],
      zoom: 14,
    });

    L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
      attribution:
        '<a target="_blank" href="https://www.openstreetmap.org/">© OpenStreetMap 貢獻者</a>',
      maxZoom: 18,
    }).addTo(this.map);
  },
};
</script>
<style lang=""></style>
