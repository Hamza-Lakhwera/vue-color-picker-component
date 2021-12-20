<template>
  <!-- The Modal -->
  <div @click="closeModal" v-show="showModal" id="myModal" class="modal">
    <!-- Modal content -->
    <div
      @click="stopPropagationHandler"
      :style="{ backgroundColor: selectedColor }"
      class="modal-content"
    >
      <div class="tab">
        <button
          class="tablinks"
          :class="{
            active: !isGradient,
          }"
          @click="changeTab(false)"
        >
          Pure
        </button>
        <button
          class="tablinks"
          :class="{
            active: isGradient,
          }"
          @click="changeTab(true)"
        >
          Gradient
        </button>
      </div>

      <div id="pure" v-if="!isGradient" class="tabcontent">
        <ColorPickerWithEyeDropper
          :selectedColor="selectedColor"
          :onColorChange="onColorChange"
          :selectedImage="selectedImage"
          :isEyeDropper="isEyeDropper"
          :closeEyeDropper="closeEyeDropper"
        />
      </div>

      <div id="gradient" v-if="isGradient" class="tabcontent">
        <ColorPickerWithGradient
          :selectedColor="selectedColor"
          :onColorChange="onColorChange"
          :selectedImage="selectedImage"
          :isEyeDropper="isEyeDropper"
          :closeEyeDropper="closeEyeDropper"
        />
      </div>
      <button class="button button2" @click="closeModal">Close</button>
    </div>
  </div>
</template>

<script>
import ColorPickerWithEyeDropper from "./colorPicker/ColorPickerWithEyeDropper.vue";
import ColorPickerWithGradient from "./colorPicker/ColorPickerWithGradient.vue";

export default {
  name: "Modal",
  data: function () {
    return {
      isGradient: false,
    };
  },
  props: [
    "showModal",
    "closeModal",
    "selectedColor",
    "onColorChange",
    "selectedImage",
    "isEyeDropper",
    "closeEyeDropper",
  ],
  components: {
    ColorPickerWithEyeDropper,
    ColorPickerWithGradient,
  },
  methods: {
    stopPropagationHandler(event) {
      event.stopPropagation();
    },
    changeTab(value) {
      this.isGradient = value;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* The Modal (background) */
.modal {
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  padding-top: 10%; /* Location of the box */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0, 0, 0); /* Fallback color */
  background-color: rgba(0, 0, 0, 0.4); /* Black w/ opacity */
}

/* Modal Content */
.modal-content {
  position: relative;
  background-color: #fff;
  margin: auto;
  padding: 20px;
  border: 1px solid #888;
  width: 60%;
  height: 60%;
  text-align: center;
  border-radius: 20px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  -webkit-animation-name: animatetop;
  -webkit-animation-duration: 0.4s;
  animation-name: animatetop;
  animation-duration: 0.4s;
}

/* Add Animation */
@-webkit-keyframes animatetop {
  from {
    top: -300px;
    opacity: 0;
  }
  to {
    top: 0;
    opacity: 1;
  }
}

@keyframes animatetop {
  from {
    top: -300px;
    opacity: 0;
  }
  to {
    top: 0;
    opacity: 1;
  }
}

/* The Close Button */
.close {
  color: white;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
}

.modal-header {
  padding: 2px 16px;
  color: white;
}

.modal-body {
  padding: 2px 16px;
}

.modal-footer {
  padding: 2px 16px;
  color: white;
}

.button {
  color: white;
  padding: 16px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  transition-duration: 0.4s;
  cursor: pointer;
  border-radius: 20px;
  position: absolute;
  bottom: 20px;
  left: 45%;
}
.button2 {
  background-color: white;
  color: black;
  border: 2px solid #008cba;
}

.button2:hover {
  background-color: #008cba;
  color: white;
}

/* Style the tab */
.tab {
  overflow: hidden;
  border: 1px solid #ccc;
  background-color: #f1f1f1;
}

/* Style the buttons inside the tab */
.tab button {
  background-color: inherit;
  float: left;
  border: none;
  outline: none;
  cursor: pointer;
  padding: 14px 16px;
  transition: 0.3s;
  font-size: 17px;
}

/* Change background color of buttons on hover */
.tab button:hover {
  background-color: #ddd;
}

/* Create an active/current tablink class */
.tab button.active {
  background-color: #ccc;
}

/* Style the tab content */
.tabcontent {
  padding: 6px 12px;
  border: 1px solid #ccc;
  border-top: none;
  height: 80%;
}
</style>
