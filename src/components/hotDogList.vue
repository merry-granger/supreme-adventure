<template>
    <ul>
        <li v-for="hotdog in hotDogs">
            <HotDogsItem :hotDog="hotdog"></HotDogsItem>
        </li>
    </ul>
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
