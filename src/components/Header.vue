<template>
  <header>
    <h1>BOOLFLIX</h1>
    <div>
      <input @keydown.enter="callEmit" id="searchInput" type="text" />
      <button @mouseup="callEmit">submit</button>
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
    callEmit() {
      const emitValue = document.getElementById("searchInput").value;
      document.getElementById("searchInput").value="";
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