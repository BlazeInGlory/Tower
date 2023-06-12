<template>
  <section class="row justify-content-center col-12">
  <div class="">
    <div class="justify-content-around my-3 bg-info rounded p-3">
      <button @click="filterBy=''" class="btn btn-outline-light w-25 mx-2">All</button>
      <button @click="filterBy='concert'" class="btn btn-outline-light w-25 mx-2">Concert</button>
      <button @click="filterBy='convention'" class="btn btn-outline-light w-25 mx-2">Convention</button>
      <button @click="filterBy='sport'" class="btn btn-outline-light w-25 mx-2">Sports</button>
      <button @click="filterBy='digital'" class="btn btn-outline-light w-25 mx-2">Digitals</button>
    </div>
  </div>
</section>
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
  name: "Home",
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
      events: computed(() => {
        if(filterBy.value == "") {
          return AppState.events
        }else {
          return AppState.events.filter(e=>filterBy.value ? e.type == filterBy.value : true)
      }
    })
  }
  },
  components: { EventCard }
}
</script>

<style scoped lang="scss">
</style>