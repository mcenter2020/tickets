<template>
<ul>
<Ticket
  v-for="(tick, i) of tickets" :key="tick"
  v-bind:tick="tick"
  v-bind:index="i"

/>
</ul>





</template>

<script>
import Ticket from '@/components/Ticket.vue'

export default {
  props: ['tickets'],
  components: {
    Ticket
  },
  }
</script>
