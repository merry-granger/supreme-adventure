<template>
 <div id="app"> 
    <ul>
        <li v-for="hotdog in hotDogs">
            <HotDogsItem :hotDog="hotdog"></HotDogsItem>
        </li>
    </ul>
 </div>
</template>

<script>
    import HotDogsItem from "./hotDogItem";

    export default {
        components: {HotDogsItem},
        props: {
            hotDogs: Array
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

</style>