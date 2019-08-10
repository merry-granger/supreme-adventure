<template>
    <div  id="app">
        <p>{{ hotdog.title }}</p>
        <div>
            <button @click="editHotDog"></button>
            <button @click="deleteFromArr"></button>
        </div>
    </div>
</template>

<script>
    import axios from "axios";

    export default {
        name: "HotDogsListItem",
        props: {
            hotdog: Object,
        },
        inject: ["hotDogAction", "update", "deleteFromArr"],
        data: () => ({
            formDialog: false,
            formMode: "editing",
        }),
        methods: {
            async editHotDog() {
                this.formDialog = true;
                this.hotDogAction(this.hotdog, this.formMode, this.formDialog)
            },
            async deleteHotDog() {
                let url = 'https://hot-dogs-ao.herokuapp.com/api/hotdog';
                try {
                    this.deleteFromArr(this.hotDog);
                    await axios.delete(url, {data: {_id: this.hotdog._id}});
                    this.update();
                } catch (e) {
                    alert(e.message);
                }
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