<template>
  <div id="app" class="d-flex flex-column">

    <HeaderComponent :genres="disksGenres" @search="filterDisks" />
    <LoaderComponent v-if="loading" />
    <MainComponent v-else-if="errorMessage.length === 0" :disksInfo="disksToDisplay" class="col flex-grow" />

    <ErrorMessageComponent v-else :errorMessage="errorMessage" />

  </div>
</template>

<script>
// Import bootstrap library
import 'bootstrap/dist/css/bootstrap.css'

// Import axios
import axios from 'axios';

import HeaderComponent from '@/components/HeaderComponent.vue'
import MainComponent from '@/components/MainComponent.vue'
import LoaderComponent from '@/components/utils/LoaderComponent.vue'
import ErrorMessageComponent from '@/components/utils/ErrorMessageComponent.vue';

export default {
  name: 'App',
  components: {
    HeaderComponent,
    MainComponent,
    LoaderComponent,
    ErrorMessageComponent
  },
  data() {
    return {
      disksApi: 'https://flynn.boolean.careers/exercises/api/array/music',
      disksInfo: [],
      disksGenres: [],
      genreToFilter: '',

      // Working Variables
      loading: true,
      errorMessage: ''
    }
  },
  created() {
    this.getDisksInfo();
  },
  methods: {

    getDisksInfo() {
      axios.get(this.disksApi)
        .then(({ status, data }) => {
          this.loading = false;
          console.log(data)

          if (status === 200) {

            this.disksInfo = data.response;

            // Memorizzo i generi musicali in un array
            this.disksInfo.forEach((disk) => {
              console.log('Disco presente: ' + disk.title);

              if (!this.disksGenres.includes(disk.genre))
                this.disksGenres.push(disk.genre)

            })

            console.log('Generi musicali presenti: ' + this.disksGenres)
          }
        })
        .catch((e) => {
          console.log(e)
          this.loading = false;
          this.errorMessage = e.code;
        })
    },
    filterDisks(genreToSearch) {
      this.genreToFilter = genreToSearch
      console.log('Filtro il genere', genreToSearch)
    }

  },
  computed: {
    disksToDisplay() {
      const array = [];

      this.disksInfo.forEach((disk) => {

        // Mostra tutti i dischi
        if (this.genreToFilter === '') {
          array.push(disk)
        }

        // Mostra i dischi del genere ricercato
        if (disk.genre === this.genreToFilter) {
          array.push(disk)
        }

      })

      return array
    }
  }

}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  height: 100vh;
}

::-webkit-scrollbar {
  display: none;
}
</style>
