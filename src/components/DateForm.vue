<template>
<div id="add-form">
    <div class="container">
        <h3 class="mt-3">Odaberite datume prijave i odjave: </h3>
        <form class="mb-3">
            <label>Check in:</label>
            <input type="date" class="input mr-2" name="checkin" v-model="dates.checkin">
            <label>Check out:</label>
            <input type="date" class="input" name="checkout" v-model="dates.checkout">
            <button @click.prevent="sendPost()" class="btn btn-primary ml-2">Provjeri</button>
        </form>
        <div class="row">
        <div v-for="room in rooms" id="rooms" class="card rooms mr-3" v-on:click="show = !show" v-bind:id="room.id" @click="sendRoom">
            <img class="card-img-top" v-bind:src="'http://127.0.0.1:8000/images/thumbnails/' + room.thumbnail">
            <h5 class="card-title">{{ room.title }}</h5>
            <p class="card-text">{{ room.quantity }}</p>
            
        </div>
        </div>
        <transition name="fade">
            <form v-if="show" @submit="checkForm">
                <div class="form-group mt-4">
                    <label>Email: </label>
                    <input type="email" class="form-control" v-model="personaldata.email">
                    <label>Broj telefona : </label>
                    <input type="text" class="form-control" v-model="personaldata.telephone">
                    <label>Ime i prezime: </label>
                    <input type="text" class="form-control" v-model="personaldata.name">
                    <button type="submit" value="Submit" class="btn btn-primary mt-2">Potvrdi</button>
                </div>
            </form>
        </transition>
        <p>{{ success_msg }}</p>
        <p v-if="errors.length">
                    <b>Greška! :</b>
                    <ul>
                    <li v-for="error in errors">{{ error }}</li>
                    </ul>
                </p>
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
            show: false,
            errors: [],
            success_msg: '',
            personaldata: {
                email: '',
                telephone: '',
                name: ''
            }
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
        },
            checkForm: function (e) {
                var personaldata = {
                    email: this.personaldata.email,
                    telephone: this.personaldata.telephone,
                    name: this.personaldata.name,
                    checkin: this.dates.checkin,
                    checkout: this.dates.checkout
                }
                if (this.personaldata.email && this.personaldata.telephone && this.personaldata.name) {
                    this.$http.post('https://127.0.0.1:8000/api/postPersonalData', personaldata).then(function (data){
                        console.log(data);
                        this.success_msg = 'Uspješno ste rezervirali!';
                        this.personaldata.email = data.body.email;
                    })
            }

      this.errors = [];

      if (!this.personaldata.email) {
        this.errors.push('Email required.');
      }
      if (!this.personaldata.telephone) {
        this.errors.push('Telephone required.');
      }
      if (!this.personaldata.name) {
        this.errors.push('Name and surname required.');
      }

      e.preventDefault();
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
.card{
    padding: 5px;
    width: 18rem;
}

.card-img-top {
    overflow: hidden;
    max-width: 300px;
    max-height: 155px;
}
</style>
