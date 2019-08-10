<template>
  <div id="app">
    Hot Dogs
    <div><button @click="add">Add new hot dog</button>
    </div>
    <hotDogList :hotDogs="hotDogs"/>
    <hotDogForms/>

  </div>

</template>

<script>
import hotDogForms from './components/hotDogForms'
import hotDogList from './components/hotDogList'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    hotDogForms,
    hotDogList
  },
  provide() {
         return {
            update: () => this.getHotDogs(),
          }
      },
  data: () => ({
          hotDogs:'',
      }),
  methods: {
          async add() {
            this.$modal.show('form');
          },
          async getHotDogs() {
              try {
                  await axios.get('https://floating-woodland-55116.herokuapp.com/api/hotDog')
                          .then( response => {
                                  this.hotDogs = response.data
                          })
              } catch (e) {
              }
          },
      },
    created() {
          this.getHotDogs();
      },
}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #1b9954;
  margin-top: 60px;
}
</style>
