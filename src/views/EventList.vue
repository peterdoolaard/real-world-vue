<template>
  <h1>Events for good</h1>
  <div class="events">
      <EventCard
        v-for="event in events"
        :key="event.id"
        :event="event"
      />
  </div>
</template>

<script>
// @ is an alias to /src
import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService'

export default {
  name: 'EventList',
  components: {
    EventCard
  },
  data () {
    return {
      events: null
    }
  },
  created () {
    EventService.getEvents()
      .then(response => {
        this.events = response.data
      })
      .catch(error => {
        console.log(error)
      })
  }
}
</script>

<style scoped lang="scss">
.events {
  align-items: center;
  display: flex;
  flex-flow: column;
}
</style>
