<template>
  <div class="container-fluid">
    <section class="row">
      <div class="col-md-4" v-for="e in events" :key="e.id">
        <EventCard :event="e"/>
      </div>
    </section>
  </div>
</template>

<!-- [ All?? 'concert', 'convention', 'sport', 'digital'] -->

<script>
import Pop from '../utils/Pop'
import { eventsService } from '../services/EventsService.js'
import { onMounted, ref} from 'vue'
import { computed } from '@vue/reactivity'
import { AppState } from '../AppState'
import EventCard from '../components/EventCard.vue'
export default {
  setup() {
    const filterBy = ref('')
      async function getEvents() {
        try {
          await eventsService.getAll()
        }
        catch (error) {
        Pop.error(error)
        }
      }
  onMounted(() => {
    getEvents()
  })
    return {
      filterBy,
        events: computed(() => AppState.events)
    }
  },
  components: { EventCard }
}
</script>

<style scoped lang="scss">
</style>