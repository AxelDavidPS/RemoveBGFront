<script setup>
import { ref } from "vue";

const emit = defineEmits(["ThereIsimg", "imgWithontBG"]);
defineProps(["Isimg", "IsimgSinBG"]);

const img_file = ref({});
const img64 = ref("");

const obtainFile = (input) => {
  img_file.value = input.target.files[0];
  const url_img = URL.createObjectURL(img_file.value);
  emit("ThereIsimg", url_img);
};

const deletBg = (e) => {
  e.preventDefault();
  const formData = new FormData();
  formData.append("file", img_file.value);

  fetch("http://127.0.0.1:5000/api/v1/img", {
    method: "POST",
    body: formData,
  })
    .then((response) => response.json())
    .then((data) => {
      img64.value = data.img
      emit("imgWithontBG", data.img);
    });
};
</script>

<template>
  <form class="container-xl mt-4 text-center">
    <label for="select-img" class="btn btn-outline-primary">Upload image</label>
    <input
      class="form-control"
      type="file"
      name="image"
      accept="image/*"
      id="select-img"
      @change="obtainFile"
      hidden
    />
    <label for="btn-submit" class="btn btn-primary ms-3" v-if="Isimg"
      >Send</label
    >
    <button type="submit" id="btn-submit" @click="deletBg" hidden></button>

    <a :href="`data:image/png;base64,${img64}`" class="btn btn-secondary ms-3" v-if="IsimgSinBG" download="img.png">Download</a>
  </form>
</template>

<style scoped></style>
