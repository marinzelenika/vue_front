<template>
<div id="add-form">
    <div class="container">
        <h3 class="mt-3">Odaberite datume: </h3>
        <form>
            <label>Check in:</label>
            <input type="date" class="input" name="checkin" v-model="dates.checkin">
            <label>Check out:</label>
            <input type="date" class="input" name="checkout" v-model="dates.checkout">
            <button @click.prevent="sendPost()" class="btn btn-primary ml-2">Provjeri</button>
        </form>
        <option v-for="room in rooms" id="rooms" class="rooms" v-bind:id="room.id" @click="sendRoom">{{ room.title }}</option>
    </div>
    
</div>
</template>

<script>
export default {
    data() {
        return {
            dates: {
            checkin: '',
            checkout: ''
        },
        rooms: [],
        roomid: ''
        }
    },

    methods: {
        sendPost() {
            var postData = {
                checkin: this.dates.checkin,
                checkout: this.dates.checkout
            }
            this.$http.post('https://127.0.0.1:8000/api/getDates', postData).then(function (data) {
                console.log(data);
                this.rooms = data.body;
            })
        },
        sendRoom(event){
            var postRooms = {roomid: event.target.id}
            this.$http.post('https://127.0.0.1:8000/api/getRoom', postRooms).then(function (event){
                console.log(postRooms);
            })
        }

    }
}
</script>

<style scoped>
.rooms{
    cursor: pointer;
}

</style>
