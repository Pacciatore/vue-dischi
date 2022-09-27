<template>
  <header>
    <div class="d-flex px-4 py-3 justify-content-between">

      <!-- Brand Logo -->
      <div class="col-1">
        <img src="@/assets/logo.png" alt="logo">
      </div>


      <!-- Genre selection research -->
      <div class="col-3 d-flex align-items-center">

        <label for="genreSelection" class="pe-2 text-white">Genere:</label>

        <select name="genreSelection" id="genreSelection" class="col-4 rounded px-1 py-2" @change.prevent="doSearch">

          <option selected value="">Tutti i generi</option>

          <option v-for="genre in genres" :key="genre" :value="genre">
            {{ genre }}
          </option>

        </select>
      </div>

    </div>
  </header>
</template>

<script>
export default {
  name: 'HeaderComponent',
  data() {
    return {
      searchGenre: ''
    }
  },
  props: {
    genres: Array
  },
  methods: {
    doSearch(event) {
      this.$emit('search', event.target.value);
    }
  }
}
</script>

<style scoped lang="scss">
@import '@/assets/style/variables.scss';

header {
  background-color: $tr-spotify-header;

  img {
    height: 50px;
    width: 50px;
  }

  // Select genre element
  #genreSelection {
    background-color: $tr-spotify-main;
    color: white;
    border-color: $tr-spotify-green;

    &:focus-visible {
      outline: none;
    }

  }

}
</style>
