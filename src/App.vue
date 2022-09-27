<template>
  <div id="app" class="d-flex flex-column">

    <HeaderComponent />
    <LoaderComponent v-if="loading" />
    <MainComponent v-else :disksInfo="disksInfo" class="col flex-grow" />

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

export default {
  name: 'App',
  components: {
    HeaderComponent,
    MainComponent,
    LoaderComponent
  },
  data() {
    return {
      disksApi: 'https://flynn.boolean.careers/exercises/api/array/music',
      disksInfo: [],
      disksGenres: [],
      loading: true
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
</style>
