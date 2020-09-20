<template>
<div id="add-form">
    <h3>Odaberite datume</h3>
    <form>
        <label>Check in:</label>
        <input type="date" class="input" name="checkin" v-model="checkin">
        <label>Check out:</label>
        <input type="date" class="input" name="checkout" v-model="checkout">
    </form>
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

    // our methods
    methods: {
        processForm: function () {
            console.log({
                checkin: this.checkin,
                checkout: this.checkout
            });
            alert('Processing!');
        }
    }
}
</script>

<style scoped>

</style>
