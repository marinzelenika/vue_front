<template>
<div id="add-form">
    <div class="container">
    <h3 class="mt-3">Odaberite datume: </h3>
    <form>
        <label>Check in:</label>
        <input type="date" class="input" name="checkin" v-model="checkin">
        <label>Check out:</label>
        <input type="date" class="input" name="checkout" v-model="checkout">
        <button v-on:click="post" class="btn btn-primary ml-2">Spremi</button>
    </form>
    </div>
</div>
</template>

<script>
export default {
    data() {
        return {
            checkin: '',
            checkout: ''
        }
    },

    
    methods: {
        post: function(){
            this.$http.post('http://127.0.0.1:8000/api/getDates',{
                checkin: this.checkin,
                checkout: this.checkout
            },{emulateJSON: true}).then(function(data){
                console.log(data);
            })
        }
        
}
}
</script>

<style scoped>

</style>
