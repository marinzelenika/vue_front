<template>
<div>
    <app-header></app-header>
    <DateForm></DateForm>
</div>
</template>

<script>
import Header from './components/Header.vue'
import DateForm from './components/DateForm.vue'
import GetRooms from './components/GetRooms.vue'

export default {
    components: {
        'app-header': Header,
        'DateForm': DateForm,
        'GetRooms': GetRooms
    },
    data() {
        return {

        }
    }
}
</script>

<style>

</style>
