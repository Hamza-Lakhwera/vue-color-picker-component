<template>
  <div class="ColorPickerEyeDropContainer">
    <color-picker
      v-model:pureColor="pureColor"
      v-model:gradientColor="gradientColor"
      v-model:isWidget="isWidget"
      v-model:format="format"
      v-model:pickerType="pickerType"
      v-model:shape="shape"
      v-model:useType="useType"
      v-model:disableHistory="disableHistory"
      v-model:roundHistory="roundHistory"
      v-model:disableAlpha="disableAlpha"
      v-model:zIndex="zIndex"
      v-model:lang="lang"
      v-model:update:gradientColor="changeGradientHandler"
    />
  </div>
</template>

<script>
export default {
  name: "ColorPickerWithGradient",
  props: [
    "selectedColor",
    "onColorChange",
    "selectedImage",
    "isEyeDropper",
    "closeEyeDropper",
  ],
  data() {
    return {
      pureColor: "red", // choose color for spot
      gradientColor:
        "linear-gradient(0deg, rgba(0, 0, 0, 1) 0%, rgba(0, 0, 0, 1) 100%)", // choose default radiant color
      isWidget: true, // true | false
      format: "rgb", // rgb | prgb | hex | hex6 | hex3 | hex4 | hex8 | name | hsl | hsv
      pickerType: "chrome", // fk, chrome
      shape: "circle", // squire | circle
      useType: "gradient", // both | pure | gradient
      disableHistory: false, // true | false
      roundHistory: false, // true | false
      disableAlpha: false, // true | false
      zIndex: 1, // number
      lang: "En", // ZH-cn | En
    };
  },
};
</script>

<style>
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

.vc-colorpicker {
  background-color: #1d2024 !important;
}
</style>
