<template>
 <modal name="form">
   <div class="form-div">
     <label for="input">Hotdog title</label>
     <input v-model="title" type="text" id="input">
     <p><button @click="add">Save</button></p>
   </div>
 </modal>
</template>

<script>
  import axios from 'axios'
export default {
  name: 'hotDogItem',
  inject: ["update"],
  data: () => ({
    title:''
  }),
  methods:{
    async add(){
      try {
          axios.post('https://floating-woodland-55116.herokuapp.com/api/hotDog',{
              title: this.title
          }).then(() =>{
              this.update();
          })
      } catch (e){

      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #1b9954;
  margin-top: 60px;
}
.form-div{
  display: flex;
  justify-content: center;
  flex-direction: column;
}
</style>
