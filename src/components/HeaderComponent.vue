<template>
  <header>
    <div class="d-flex px-4 py-3 justify-content-between">

      <!-- Brand Logo -->
      <div class="col-1">
        <img src="@/assets/logo.png" alt="logo">
      </div>


      <!-- Genre selection research -->
      <div class="col-5 d-flex align-items-center">

        <SelectFilterComponent :filter="searchGenre" @search="doSearch" class="col-4" />

        <SelectFilterComponent :filter="searchAuthor" @search="doSearch" class="col-4" />

      </div>

    </div>
  </header>
</template>

<script>
import SelectFilterComponent from '@/components/utils/SelectFilterComponent.vue';
export default {
  name: "HeaderComponent",
  props: {
    searchGenre: Object,
    searchAuthor: Object
  },
  methods: {
    doSearch(filter) {
      this.$emit('search', filter)
    }
  },
  components: { SelectFilterComponent }
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
