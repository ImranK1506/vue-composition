<script setup>
  import EventCard from '@/components/EventCard.vue';
  import { ref, onMounted } from 'vue';
  import EventService from '@/services/EventService';

  const props = defineProps({
    page: { required: true }
  })

  const events = ref(null)

  onMounted(() => {
    EventService.getEvents(2, props.page)
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
