<template>
  <div class="popup">
    <div class="popup__text"><p>Новый клиент успешно создан</p></div>
    <div class="popup__button"><button @click="close()">X</button></div>
  </div>
</template>

<script>
export default {
  name: "MyForm",
  data: () => ({}),
  methods: {
    close() {
      this.$emit("active", false);
    },
  },
};
</script>

<style scoped lang="scss">
$primaryColor: #5596d3;
$maxWidthContainer: 1170;
$md1: $maxWidthContainer + 12;
$md2: 991.98;
$md3: 767.98;
$md4: 479.98;
.popup {
  width: 50rem;
  height: 20rem;
  background: white;
  border: 2px solid $primaryColor;
  z-index: 10;
  position: fixed;
  top: calc(50% - #{10rem});
  left: calc(50% - #{25rem});
  border-radius: 10px;
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  font-size: 2.5rem;

  @media (max-width: $md4 + px) {
    width: 25rem;
    height: 10rem;
    top: calc(50% - #{5rem});
    left: calc(50% - #{12.5rem});
    font-size: 1.5rem;
  }

  &__text {
    padding: 0.5rem 3rem;
    color: black;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;

    // text-align: right;
    // font-size: 2rem;
  }

  &__button {
    padding: 1rem;
    button {
      color: red;
      border: none;
      background: transparent;
      font-size: 2rem;
    }
  }
}
</style>