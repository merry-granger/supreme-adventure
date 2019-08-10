<template>
 <div id="app"> 
    <ul class="ul-style">
        <li v-for="hotdog in hotDogs" :key="hotdog._id">
            <hotDogItem :hotdog="hotdog" ></hotDogItem>
        </li>
    </ul>
 </div>
</template>

<script>
    import hotDogItem from "./hotDogItem";

    export default {
        components: {hotDogItem},
        props: {
            hotDogs:''
        },
    };
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
.ul-style{
    list-style: none;
}
</style>