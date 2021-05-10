<template>
  <div>
    <h1>Events</h1>
    <event-card
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    ></event-card>
  </div>
</template>
<script>
import EventCard from '~/components/EventCard.vue'
// import EventService from '~/services/EventService.js'
import { mapState } from 'vuex'

export default {
  components: { EventCard },
  head() {
    return {
      title: 'Event Listing',
    }
  }, 
  async fetch({ store, error }) { // Nuxt Extra Hook 
    try {
      await store.dispatch('events/fetchEvents')
    }
    catch(e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time. Please try again.'
      })
    }
  }, 
  computed: mapState({
    events: state => state.events.events
  })
}
</script>