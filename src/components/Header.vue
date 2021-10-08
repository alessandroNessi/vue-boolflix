<template>
  <header>
    <h1>BOOLFLIX</h1>
    <div>
      <input @keydown.enter="callEmit" ref="searchInput" type="text" placeholder="inserisci il film da cercare"/>
      <button @mouseup="callEmit">cerca</button>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {};
  },
  methods: {
    /**emit the value of the input in app */
    callEmit() {
      const emitValue = this.$refs.searchInput.value;
      this.$refs.searchInput.value="";
      if (emitValue != "") {
        this.$emit("emittedSearch", emitValue);
      }
    },
  },
};
</script>

<style scoped lang="scss">
@import '../assets/style/common.scss';
header {
  height: $header_height;
  background-color: $black_bgr;
  padding: 0 4rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  h1{
      color: rgb(175, 0, 0);
  }

}
</style>