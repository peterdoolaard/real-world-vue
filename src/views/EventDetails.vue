<template>
  <article v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </article>
</template>

<script>
import EventService from '@/services/EventService'

export default {
  name: 'EventDetails',
  props: ['id'],
  data () {
    return {
      event: null
    }
  },
  created () {
    EventService.getEvent(this.id)
      .then(response => {
        this.event = response.data
      })
      .catch(error => {
        console.log(error)
      })
  }
}
</script>

<style scoped>

</style>
