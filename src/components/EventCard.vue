<template>
  <div class="event-card">
    <RouterLink class="event-link" :to="{name: 'EventDetails', params: { id: event.id }}">
      <header>
        <span>@{{ event.time }} on {{ event.date }}</span>
        <h2>{{ event.title }}</h2>
      </header>
    </RouterLink>
  </div>
</template>

<script>
export default {
  name: 'EventCard',
  props: {
    event: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped
       lang="scss">
.event-card {
  border: 1px solid hsl(0 0% 0% / 0.8);
  cursor: pointer;
  inline-size: 20rem;
  margin-block-end: 1rem;
  padding: 1.25rem;
  transition: transform 250ms ease-in-out;

  &:hover {
    box-shadow: 0 3px 12px 0 hsl(0 0% 0% / 0.2);
    transform: scale(1.01);
  }

  .event-link {
    color: hsl(210deg 29% 24%);
    text-decoration: none;
  }
}
</style>
