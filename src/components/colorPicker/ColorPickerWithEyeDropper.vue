<template>
  <div class="ColorPickerEyeDropContainer">
    <ColorPicker
      :theme="theme"
      :color="color"
      :sucker-hide="false"
      :sucker-canvas="suckerCanvas"
      :sucker-area="suckerArea"
      @changeColor="changeColor"
      @openSucker="openSucker"
    />
    <img v-if="isOpenSucker" class="imagePicker" ref="cover" />
  </div>
</template>

<script>
import { ColorPicker } from "vue-color-kit";
import "vue-color-kit/dist/vue-color-kit.css";

export default {
  name: "ColorPickerWithEyeDropper",
  components: {
    ColorPicker,
  },
  data() {
    return {
      color: "yellow",
      suckerCanvas: null,
      suckerArea: [],
      isOpenSucker: true,
      theme: "dark",
    };
  },
  props: [
    "selectedColor",
    "onColorChange",
    "selectedImage",
    "isEyeDropper",
    "closeEyeDropper",
  ],
  methods: {
    changeColor(_color) {
      const { r, g, b, a } = _color.rgba;
      this.color = `rgba(${r}, ${g}, ${b}, ${a})`;
      this.onColorChange(this.color);
    },
    openSucker(isOpen) {
      if (isOpen) {
        this.isOpenSucker = isOpen;
        if (isOpen) {
          setTimeout(() => {
            const cover = this.$refs.cover;
            cover.onload = () => {
              if (!this.isOpenSucker) {
                return;
              }
              const coverRect = cover.getBoundingClientRect();
              const canvas = this.createCanvas(cover, coverRect);
              document.body.appendChild(canvas);
              this.suckerCanvas = canvas;
              this.suckerArea = [
                coverRect.left,
                coverRect.top,
                coverRect.left + coverRect.width,
                coverRect.top + coverRect.height,
              ];
            };
            cover.setAttribute("crossorigin", "Anonymous");
            cover.width = "800";
            cover.style.display = "block";
            cover.src = this.selectedImage;
          }, 10);
        }
      } else {
        if (!this.suckerCanvas) return;
        this.suckerCanvas.remove();
        const cover = this.$refs.cover;
        cover.src = null;
        cover.width = "0";
        cover.style.display = "none";
      }
    },
    createCanvas(cover, coverRect) {
      const canvas = document.createElement("canvas");
      const ctx = canvas.getContext("2d");
      canvas.width = coverRect.width;
      canvas.height = coverRect.height;
      ctx.drawImage(cover, 0, 0, coverRect.width, coverRect.height);
      Object.assign(canvas.style, {
        position: "absolute",
        left: coverRect.left + "px",
        top: coverRect.top + "px",
        opacity: 0,
        zIndex: 99,
        cursor: "crosshair",
      });
      return canvas;
    },
  },
  beforeUnmount() {
    this.closeEyeDropper();
    if (!this.suckerCanvas) return;
    const element = document.getElementsByClassName("active sucker");
    element[0].dispatchEvent(new Event("click"));
  },
  mounted() {
    if (this.isEyeDropper) {
      setTimeout(() => {
        const element = document.getElementsByClassName("sucker");
        element[0].dispatchEvent(new Event("click"));
      }, 500);
    }
  },
};
</script>

<style scoped>
.ColorPickerEyeDropContainer {
  width: 100%;
  margin: auto;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  gap: 20px;
  height: 100%;
}
.imagePicker {
  cursor: crosshair;
}
</style>
