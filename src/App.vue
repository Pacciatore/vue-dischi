<template>
  <div id="app" class="d-flex flex-column">

    <HeaderComponent />
    <MainComponent :diskInfo="diskInfo" class="col flex-grow" />

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
      diskInfo: []
    }
  },
  mounted() {
    axios.get(this.disksApi)
      .then((response) => {
        console.log(response.data)
        this.diskInfo = response.data.response;
        console.log(this.diskInfo)
      })
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
