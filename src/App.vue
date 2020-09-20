<template>
<div>
    <app-header></app-header>
    <DateForm></DateForm>
</div>
</template>

<script>
import Header from './components/Header.vue'
import DateForm from './components/DateForm.vue'

export default {
    components: {
        'app-header': Header,
        'DateForm': DateForm
    },
    data() {
        return {

        }
    }
}
</script>

<style>

</style>
