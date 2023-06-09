<template>
  <div class="mt-3 elevation-5 rounded selectable card" @click="goTo" :title="event.name">
    <div class="card">
      <img class="img-fluid" :src="event.coverImg" alt="Event Image">
      <h3 class="text-center">{{event.name}}</h3>
    </div>
  </div>
</template>

<script>
import { router } from '../router'
// import { logger } from "../utils/Logger.js"
// import { eventsService } from "../services/EventsService.js"
// import { ticketsService } from "../services/TicketsService.js"
export default {
  props: {event: {type: Object, required: true}},
setup(props) {
  return {
    goTo(){
      router.push({name: 'EventDetails', params: {eventId: props.event.id}})
    }
  }
},
}
</script>

<style>
</style>