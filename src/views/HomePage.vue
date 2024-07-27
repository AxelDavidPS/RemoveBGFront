<script setup>
import { ref } from "vue";
import Form from "../components/Form.vue";

const img_url = ref("");
const img_urlSinBG = ref("");
const Isimg = ref(false);
const IsimgSinBG = ref(false);

const ThereIsimg = (img) => {
  IsimgSinBG.value = false;
  Isimg.value = true;
  img_url.value = img;
};

const imgWithontBG = (img64) => {
  IsimgSinBG.value = true;
  img_urlSinBG.value = img64;
};
</script>

<template>
  <div class="container mt-3 text-center">
    <h1 class="text-center">Remove BackGround</h1>
    <h2 class="text-center"><i>by Axel David Plascencia Silva</i></h2>
    <Form
      @ThereIsimg="ThereIsimg"
      @imgWithontBG="imgWithontBG"
      :Isimg="Isimg"
      :IsimgSinBG="IsimgSinBG"
    />
    <div class="row justify-content-center">
      <img
        :src="img_url"
        alt="img to remove BackGround"
        class="my-3 mx-auto rounded col-xl-4 col-lg-6 col-md-6 img"
        v-if="Isimg"
        id="img"
      />
      <img
        :src="`data:image/png;base64,${img_urlSinBG}`"
        alt="image without BackGround"
        v-if="IsimgSinBG"
        class="my-3 mx-auto rounded col-xl-4 col-lg-6 col-md-6 img"
      />
    </div>
  </div>
</template>

<style scoped></style>
