<template>
  <div id="app" class="d-flex flex-column">

    <HeaderComponent />
    <MainComponent :disksInfo="disksInfo" class="col flex-grow" />

  </div>
</template>

<script>
// Import bootstrap library
import 'bootstrap/dist/css/bootstrap.css'

// Import axios
import axios from 'axios';

import HeaderComponent from '@/components/HeaderComponent.vue'
import MainComponent from '@/components/MainComponent.vue'

export default {
  name: 'App',
  components: {
    HeaderComponent,
    MainComponent
  },
  data() {
    return {
      disksApi: 'https://flynn.boolean.careers/exercises/api/array/music',
      disksInfo: [],
      disksGenres: []
    }
  },
  created() {
    this.getDisksInfo();
  },
  methods: {

    getDisksInfo() {
      axios.get(this.disksApi)
        .then((response) => {
          console.log(response.data)
          this.disksInfo = response.data.response;

          // Memorizzo i generi musicali in un array
          this.disksInfo.forEach((disk) => {
            console.log('Disco presente: ' + disk.title);

            if (!this.disksGenres.includes(disk.genre))
              this.disksGenres.push(disk.genre)
          })

          console.log('Generi musicali presenti: ' + this.disksGenres)

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
