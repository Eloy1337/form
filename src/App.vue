<template>
  <div class="container" id="app">
    <my-form @success="formsuccess" />
    <popup v-if="form" @active="closepopup" />
  </div>
</template>

<script>
import MyForm from "./components/MyForm.vue";
import Popup from "./components/Popup.vue";

export default {
  name: "App",
  data: () => ({
    form: false,
  }),
  components: {
    MyForm,
    Popup,
  },
  methods: {
    formsuccess(tmp) {
      this.form = tmp;
      console.log(tmp);
    },
    closepopup() {
      this.form = false;
    },
  },
};
</script>

<style lang="scss">
// $primaryColor: #7ed321;
$primaryColor: #5596d3;
$maxWidthContainer: 1170;
$md1: $maxWidthContainer + 12;
$md2: 991.98;
$md3: 767.98;
$md4: 479.98;

*,
*:before,
*:after {
  box-sizing: border-box;
}

html {
  font-size: 10px;
}

body {
  font-family: "Roboto", sans-serif;
  // 400 and 700
  font-size: 1.5rem;
  padding: 1rem;
  margin: 0;
  color: #b9b9b9;
  background-color: #e3e3e3;
}

.container {
  max-width: 57rem;
  padding: 1rem 3rem 2rem 3rem;
  margin: 0em auto;
  background-color: #fff;
  border-radius: 4.2px;

  @media (max-width: $md4 + px) {
    padding: 1rem 0.5rem;
  }
}
</style>
