<template>
  <main>
    <div class="container">
      <!-- films -->
      <div class="type_container">
        <div class="row_title">
          <h2>FILMS</h2>
          <select @change="Filtering('film')" name="filmselect" id="filmselect">
            <option value="">tutti i generi</option>
            <option
              v-for="(element, index) in this.filmsGenres"
              :key="index"
              :value="element.id"
            >
              {{ element.name }}
            </option>
          </select>
        </div>
        <div class="row_container">
          <div class="row">
            <Card
              class="card__film col-xxl-2 col-xl-3 col-lg-4 col-md-6 col-12"
              v-for="(element, index) in this.filmsArray"
              :key="index"
              :class="{ 'd-none': !element.visibility }"
              :filmObject="element"
            />
          </div>
        </div>
      </div>

      <!-- series -->
      <div class="type_container">
        <div class="row_title">
          <h2>SERIE</h2>
          <select @change="Filtering('serie')" name="serieselect" id="serieselect">
            <option value="">tutti i generi</option>
            <option
              v-for="(element, index) in this.seriesGenres"
              :key="index"
              :value="element.id"
            >
              {{ element.name }}
            </option>
          </select>
        </div>
        <div class="row_container">
          <div class="row">
            <Card
              class="card__serie col-xxl-2 col-xl-3 col-lg-4 col-md-6 col-12"
              v-for="(element, index) in this.seriesArray"
              :key="index"
              :class="{ 'd-none': !element.visibility }"
              :filmObject="element"
            />
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import Card from "./Card.vue";
export default {
  name: "Main",
  components: {
    Card,
  },
  props: {
    filmsArray: Array,
    seriesArray: Array,
    seriesGenres: Array,
    filmsGenres: Array,
  },
  data() {
    return {};
  },
  methods: {
    Filtering(type) {
      let genre, array;
      if (type == "film") {
        genre = parseInt(document.getElementById("filmselect").value);
        array = this.filmsArray;
      } else if (type == "serie") {
        genre = parseInt(document.getElementById("serieselect").value);
        array = this.seriesArray;
      }
      array.forEach((element) => {
        console.log(element);
        console.log(genre);
        if (element.genre_ids.includes(genre) || isNaN(genre)) {
          element.visibility = true;
        } else {
          element.visibility = false;
        }
      });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/style/common.scss";
// @import '~bootstrap/scss/bootstrap.scss';
.d-none{
    display: none;
}
main {
  .type_container {
    padding-bottom: 80px;
  }
  height: calc(100vh - $header_height);
  background-color: $gray_bgr;
  overflow: auto;
  h2 {
    color: $text_color;
    text-align: center;
    padding: 10px;
  }
  .row_title {
    margin-top: 30px;
    margin-bottom: -30px;
    display: flex;
    justify-content: center;
    align-items: center;
    select {
      height: 2rem;
    }
  }
}
.row {
  &_container {
    transform: rotate(-90deg) translateY(30px) translateX(-500px);
    transform-origin: left top;
    height: 430px;
    width: 300px;
  }
  &::-webkit-scrollbar {
    display: none;
  }
  border: 1px solid #aaa;
  height: calc(100vw - 60px);
  width: 432px;
  overflow: auto;
}
</style>