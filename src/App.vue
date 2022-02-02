<template>
  <div id="app">
    <img style="display: none" ref="img" :src="image" />
    <input type="file" @change="uploadImage" />
    <canvas style="width: 300px; height: 500px" id="canvas"></canvas>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      image: "",
    };
  },
  components: {},
  methods: {
    uploadImage(e) {
      const file = e.target.files[0];
      this.image = URL.createObjectURL(file);
      let canvas = document.getElementById("canvas");
      let ctx = canvas.getContext("2d");
      let self = this;
      this.$refs.img.onload = function () {
        let iw = self.$refs.img.width;
        let ih = self.$refs.img.height;
        ctx.drawImage(this, 0, 0, 300, (ih * 300) / iw);
        ctx.save();
        let imageData = ctx.getImageData(0, 0, 300, 500);
        console.log(imageData.data);
      };
    },
  },
};
</script>

<style>
</style>
