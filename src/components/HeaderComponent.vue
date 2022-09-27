<template>
  <header>
    <div class="d-flex px-4 py-3 justify-content-between">

      <!-- Brand Logo -->
      <div class="col-1">
        <img src="@/assets/logo.png" alt="logo">
      </div>


      <!-- Genre selection research -->
      <div class="col-3 d-flex align-items-center">
        <select name="genreSelection" id="genreSelection" class="col-4 rounded p-1">

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
  props: {
    genres: Array
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
