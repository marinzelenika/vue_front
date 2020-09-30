<template>
<div id="add-form">
    <div class="container">
        <h3 class="mt-3">Odaberite datume: </h3>
        <form class="mb-3">
            <label>Check in:</label>
            <input type="date" class="input mr-2" name="checkin" v-model="dates.checkin">
            <label>Check out:</label>
            <input type="date" class="input" name="checkout" v-model="dates.checkout">
            <button @click.prevent="sendPost()" class="btn btn-primary ml-2">Provjeri</button>
        </form>
        <div v-for="room in rooms" id="rooms" class="rooms" v-on:click="show = !show" v-bind:id="room.id" @click="sendRoom">
            {{ room.title }}

        </div>
        <transition name="fade">
            <form v-if="show">
                <div class="form-group mt-4">
                    <label>Email: </label>
                    <input type="email" class="form-control">
                    <label>Broj telefona : </label>
                    <input type="text" class="form-control">
                    <label>Ime i prezime: </label>
                    <input type="text" class="form-control">
                    <button type="submit" class="btn btn-primary mt-2">Potvrdi</button>
                </div>
            </form>
        </transition>
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
            roomid: '',
            show: false
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
        sendRoom(event) {
            var postRooms = {
                roomid: event.target.id
            }
            this.$http.post('https://127.0.0.1:8000/api/getRoom', postRooms).then(function (event) {
                console.log(postRooms);
            })
        }

    }
}
</script>

<style scoped>
.rooms {
    cursor: pointer;
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity .5s;
}

.fade-enter,
.fade-leave-to

/* .fade-leave-active below version 2.1.8 */
    {
    opacity: 0;
}
</style>
