<template>
  <h1>Events for good</h1>
  <div class="events">
      <EventCard
        v-for="event in events"
        :key="event.id"
        :event="event"
      />
    <div class="pagination">
      <RouterLink
        v-show="page != 1"
        :to="{ name: 'EventList', query: { page: page - 1 } }"
        rel="prev"
        >&#60; Previous
      </RouterLink>
      <nav class="pages">
        Pages:
        <ul>
          <li v-for="pageNo in totalPages" :key="pageNo">
            <RouterLink
              :to="{ name: 'EventList', query: { page: pageNo } }"
            >
              {{ pageNo }}
            </RouterLink>
          </li>
        </ul>
      </nav>
      <RouterLink
        v-show="hasNextPage"
        :to="{ name: 'EventList', query: { page: page + 1 } }"
        rel="next"
        >Next &#62;
      </RouterLink>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService'
import { watchEffect } from 'vue'

export default {
  name: 'EventList',
  props: ['page'],
  components: {
    EventCard
  },
  data () {
    return {
      events: null,
      totalEvents: 0
    }
  },
  created () {
    watchEffect(() => {
      this.events = null
      EventService.getEvents(2, this.page)
        .then(response => {
          this.events = response.data
          this.totalEvents = response.headers['x-total-count']
        })
        .catch(error => {
          console.log(error)
        })
    })
  },
  computed: {
    hasNextPage () {
      return this.page < this.totalPages
    },
    totalPages () {
      return Math.ceil(this.totalEvents / 2)
    }
  }
}
</script>

<style scoped lang="scss">
.events {
  align-items: center;
  display: flex;
  flex-flow: column;
  inline-size: max-content;
  margin-inline: auto;
}

.pagination {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  inline-size: 100%;

  a {
    color: inherit;
    text-decoration: none;
  }

  [rel='prev'] {
    grid-column: 1;
    margin-inline-end: auto;
  }

  nav {
    column-gap: 0.5rem;
    display: flex;
    grid-column: 2;

    ul {
      display: flex;
      column-gap: 1rem;
      list-style: none;
      margin: 0;
      padding: 0;

      a {
        display: inline-block;
        text-decoration: underline;

        &:hover, .isActive  {
          font-weight: bold;
        }
      }
    }
  }

  [rel='next'] {
    grid-column: 3;
    margin-inline-start: auto;
  }
}
</style>
