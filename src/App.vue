<template>
  <div id="app">
    Hot Dogs
    <div><button @click="add">Add new hot dog</button>
    </div>
    <HotDogsList :hotDogs="hotDogs"/>
    <HotDogForms :hotDog="hotDog" :formMode="formMode" :formDialog="formDialog" @unshift="unshiftArray" @edit="editInArr"/>

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
            hotDogAction: (hotDog, formMode, formDialog) => {
                  this.hotDog = {...hotDog};
                  this.formMode = formMode;
                  this.formDialog = formDialog;
         },
            deleteFromArr: (hotDog) => {
                  this.hotDogs = this.hotDogs.filter(item => item._id !== hotDog._id);
              }
          }
      },
  data: () => ({
          hotDogs: [],
          index: 0,
          hotDog: {
              title: ""
          },
          formMode: "",
          formDialog: false,
      }),
  methods: {
          async add() {
              this.formDialog = true;
              this.formMode = 'adding';
          },
          async getHotDogs() {
              let url = 'https://floating-woodland-55116.herokuapp.com/api/hotDog';
              try {
                  let response = await axios.get(url);
                  this.hotDogs = response.data.reverse();
              } catch (e) {
                  alert(e.message);
              }
          },
          unshiftArray(hotDog) {
              this.hotDogs.unshift(hotDog);
          },
          editInArr(hotDog) {
              this.hotDogs.find(item => {
                  if (item._id === hotDog._id)
                      item.title = hotDog.title;
              });
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
