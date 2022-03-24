<template>
  <transition name="modal">
    <div class="modal-mask" v-show="showModal">
      <!-- 為了可以關閉燈箱，加上@click.self="close" -->
      <div class="modal-wrapper" @click.self="close">
        <div class="modal-container">
          <div class="modal-body">
            <!-- 先隨意放 -->
            <div>HELLO</div>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>
<script>
export default {
  name: "Lightbox",
  computed: {
    showModal: {
      get() {
        return this.$store.state.showModal;
      },
      set(value) {
        this.$store.commit("setshow<odal", value);
      },
    },
  },
  methods: {
      close(){
          this.showModal = false;
      }
  },
};
</script>
<style scoped lang="scss">
.modal-mask {
  position: fixed;
  z-index: 100;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .65);
  display: table;
  transition: opacity .3s ease;
}
.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}
.modal-container {
  width: 520px;
  margin: 0px auto;
  padding: 10px 30px;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, .3);
  transition: all .3s ease;
  font-family: Helvetica, Arial, sans-serif;
}
.modal-body {
  color: #42b983;
  margin: 20px 0;
}
</style>

<style>
.modal-enter {
  opacity: 0;
}
.modal-leave-active {
  opacity: 0;
}
.modal-enter .modal-container,
.modal-leave-active .modal-container {
  transform: scale(1.1);
}
</style>

<style lang="scss" scoped>
.store-name {
  font-size: 1.6rem;
  font-weight: bold;
  line-height: 1.5;
}
.title{
  font-weight: 500;
  margin-bottom: .5rem;
  line-height: 1.7;
}
table {
  border-spacing: 0;
  border-radius: 3px;
  width: 100%;
  margin-bottom: 1rem;
}
th{
  background-color: #42b983;
  color: #fff;
}
td, th{
  padding: .3em;
  text-align: center;
  line-height: 1.5rem;
}
</style>