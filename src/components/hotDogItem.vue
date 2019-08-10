<template>
    <div  id="app">
        <p>{{ hotdog.title }}</p>
        <div>
            <button @click="deleteHotDog">Remove</button>
            <button @click="editHotDog">Edit</button>
            <input v-model="newTitle" type="text">
        </div>
    </div>
</template>

<script>
    import axios from "axios";

    export default {
        name: "hotDogItem",
        props: {
            hotdog: '',
        },
            inject: ["update"],
        data: () => ({
            newTitle:''
        }),
        methods: {
            async editHotDog() {
                    if(this.newTitle===''){
                        this.newTitle='Default hotdog name'
                    }
                    await axios.put('https://floating-woodland-55116.herokuapp.com/api/hotDog',{
                        data:{
                            title:this.newTitle,
                            id: this.hotdog._id
                        }
                    });
                    this.update();
            },
             async deleteHotDog() {
                    await axios.delete('https://floating-woodland-55116.herokuapp.com/api/hotDog',{
                        data:{
                            id: this.hotdog._id
                        }
                    });
                    this.update();
            }
        }
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