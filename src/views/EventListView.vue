<script>
  import EventCard from '@/components/EventCard.vue';
  import { watchEffect } from 'vue';
  import EventService from '@/services/EventService';

  export default {
    name: 'event-list',
    props: ['page'],
    components: {
      EventCard
    },
    data() {
      return {
        events: null,
        totalEvents: 0,
      }
    },
    created() {
      watchEffect(() => {
        this.events = null;
        EventService.getEvents(2, this.page)
          .then((res) => {
            this.events = res.data
            this.totalEvents = res.headers['x-total-count']
          })
          .catch((error) => {
            console.log(error)
          })
      })
    },
    computed: {
      hasNextPage() {
        let totalPages = Math.ceil(this.totalEvents / 2)
        return this.page < totalPages
      }
    }
  }
</script>

<template>
  <main>
      <h1>Events</h1>
      <div class="events">
        <EventCard v-for="event in events" :key="event.id" :event="event" />

          <div class="pagination">
            <router-link
                    id="page-prev"
                    :to="{ name: 'event-list', query: { page: page - 1 }}"
                    rel="prev"
                    v-if="page !== 1"
                    >
                &#60; Previous page
            </router-link>

            <router-link
                    id="page-next"
                    :to="{ name: 'event-list', query: { page: page + 1 }}"
                    rel="next"
                    v-if="hasNextPage"
            >
                Next page &#62;
            </router-link>
          </div>
    </div>
  </main>
</template>

<style>
  .events {
      display: flex;
      flex-direction: column;
      align-items: center;
  }
  .pagination {
      display: flex;
      width: 290px;
  }
  .pagination a {
      flex: 1;
      text-decoration: none;
      color: #2c3e50;
  }

  #page-prev {
      text-align: left;
  }

  #page-next {
      text-align: right;
  }
</style>
