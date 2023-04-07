<script setup>
  import EventCard from '@/components/EventCard.vue';
  import { ref, onMounted } from 'vue';
  import axios from 'axios';

  const events = ref(null)

  onMounted(() => {
    axios
      .get('https://my-json-server.typicode.com/ImranK1506/vue-composition/events')
      .then((res) => {
        events.value = res.data
      })
      .catch((error) => {
        console.log(error)
      })
  })
</script>

<template>
  <main>
      <h1>Events</h1>
      <div class="events">
        <EventCard v-for="event in events" :key="event.id" :event="event" />
    </div>
  </main>
</template>

<style>
  .events {
      display: flex;
      flex-direction: column;
      align-items: center;
  }
</style>
