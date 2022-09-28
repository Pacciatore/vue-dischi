<template>
  <div id="app" class="d-flex flex-column">

    <HeaderComponent :searchGenre="genreArchive" :searchAuthor="authorArchive" @search="filterDisks" />
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
      genreArchive: {
        name: 'Genere',
        elements: []
      },
      authorArchive: {
        name: 'Autore',
        elements: []
      },
      searchFilter: '',

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

              if (!this.genreArchive.elements.includes(disk.genre))
                this.genreArchive.elements.push(disk.genre)

              if (!this.authorArchive.elements.includes(disk.author))
                this.authorArchive.elements.push(disk.author)

            })

            console.log('Generi musicali presenti: ' + this.genreArchive.elements)
          }
        })
        .catch((e) => {
          console.log(e)
          this.loading = false;
          this.errorMessage = e.code;
        })
    },
    filterDisks(elementToSearch) {
      this.searchFilter = elementToSearch
      console.log('Filtro gli elementi: ', elementToSearch)
    },

    // Value Checkers
    hasValidGenre(disk) {
      return disk.genre === this.searchFilter;
    },
    hasValidAuthor(disk) {
      return disk.author === this.searchFilter;
    }

  },
  computed: {
    disksToDisplay() {
      const array = [];

      this.disksInfo.forEach((disk) => {

        // Mostra tutti i dischi
        if (this.searchFilter === '') {
          array.push(disk)
        }

        // Mostra i dischi del genere ricercato
        if (this.hasValidGenre(disk)) {
          array.push(disk)
        } else if (this.hasValidAuthor(disk)) {
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
