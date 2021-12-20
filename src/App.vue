<template>
  <div class="container">
    <div class="colorPickerDimensionController">
      <div class="colorPickerFieldContainer">
        <div
          class="selectedColor"
          :style="{ backgroundColor: selectedColor }"
          @click="toggleModal"
        ></div>
        <input
          class="colorPickerInput"
          type="text"
          :value="selectedColor ?? 'Fill'"
        />
        <img
          class="colorPickerEyeDropper"
          src="assets/eye-dropper.png"
          alt="Eye dropper"
          @click="openEyeDropper"
        />
      </div>
    </div>
  </div>

  <!-- Trigger/Open The Modal -->
  <Modal
    :showModal="showModal"
    :closeModal="toggleModal"
    :selectedColor="selectedColor"
    :onColorChange="onColorChange"
    :selectedImage="selectedImage"
    :isEyeDropper="isEyeDropper"
    :closeEyeDropper="closeEyeDropper"
  />
</template>

<script>
import Modal from "./components/Modal.vue";
// import imgCover from "./assets/dummy/demo3.jpg";
// import imgSvg from "./assets/dummy/demo1.svg";
import imgPng from "./assets/dummy/demo2.png";

export default {
  name: "App",
  components: {
    Modal,
  },
  data() {
    return {
      showModal: false,
      selectedColor: "#5190dc",
      selectedImage: imgPng,
      isEyeDropper: false,
    };
  },
  methods: {
    toggleModal() {
      this.showModal = !this.showModal;
    },
    onColorChange(_color) {
      this.selectedColor = _color;
    },
    openEyeDropper() {
      this.isEyeDropper = true;
      this.showModal = true;
    },
    closeEyeDropper() {
      this.isEyeDropper = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.color-picker-component-wrapper {
  margin: auto;
  height: 100%;
  position: relative;
  margin-left: 40%;
}

.container {
  background-color: yellow;
  height: 100%;
  width: 100%;
  position: relative;
}
.colorPickerDimensionController {
  width: 500px;
  height: auto;
  margin: auto;
  position: absolute;
  top: 40%;
  left: 40%;
}
.colorPickerFieldContainer {
  width: 100%;
  height: 25px;
  padding: 15px 30px;
  background-color: #f6f6f6;
}
.selectedColor {
  width: 70px;
  height: 25px;
  background-color: black;
  float: left;
  cursor: pointer;
}
.colorPickerInput {
  float: left;
  background-color: #f6f6f6;
  border: none;
  margin-left: 7%;
  line-height: 24px;
  color: #a1a1a0;
  font-size: 20px;
}
.colorPickerInput:focus-visible {
  outline: none;
}
.colorPickerEyeDropper {
  float: right;
  width: 30px;
  cursor: pointer;
}
</style>
