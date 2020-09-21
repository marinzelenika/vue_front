<template>
  <div id="show-rooms">
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
            rooms:[]
        }
    },
    methods: {
        
    },
    created() {
        this.$http.get('https://jsonplaceholder.typicode.com/posts').then(function(){
            console.log(data);
            this.rooms = data.body.slice(0,10);
        })
    },

}
</script>

<style>

</style>