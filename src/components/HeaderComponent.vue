<template>
  <header>
    <div class="d-flex px-4 py-3">

      <div class="col-1">
        <img src="@/assets/logo.png" alt="logo">
      </div>

    </div>
  </header>
</template>

<script>
export default {
  name: 'HeaderComponent',
  props: {
    genre: String
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

}
</style>
