<template>
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>
<script>
import EventCard from '../components/EventCard'
export default {
  components: { EventCard },
  head() {
    return {
      title: 'Event Listing'
    }
  },
  asyncData({ $axios, error }) {
    return $axios
      .get('http://localhost:3000/events')
      .then(response => {
        return {
          events: response.data
        }
      })
      .catch(e => {
        error({
          statusCode: 503,
          message:
            'Unable to fetch the events at this time. Please try again later.'
        })
      })
  }
}
</script>
