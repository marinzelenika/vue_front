<template>
<div id="show-rooms" class="container">
    <h2>Available Rooms</h2>
    <div v-for="room in rooms" class="single-room">
        {{ room.title }}
    </div>
</div>
</template>

<script>
export default {
    data() {
        return {
            rooms: []
        }
    },
    methods: {

    },
    created() {
        this.$http.get('https://127.0.0.1:8000/api/r').then(res => {
            console.log(this.data);
            this.rooms = res.body.slice(0, 10);
        })
    },

}
</script>

<style>

</style>
