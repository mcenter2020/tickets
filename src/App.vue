<template>
  <div id="app">
  <h1>Приложение для добавления тиккетов</h1><br>
  <hr>
  <AllTickets v-bind:tickets="tickets" />
  <hr>
  <button type="button" class="btn btn-primary" id="show-modal" @click="showModal = true">Добавить тиккет</button>
    <modal v-if="showModal" @close="showModal = false" @add-ticket="addNewTicket">
      <h3 class="font-weight-bold" slot="header">Новый тикет</h3>
    </modal>

  </div>
</template>

<script>

import AllTickets from '@/components/AllTickets.vue'
import modal from '@/components/Modal.vue';


export default {
  name: 'App',
  data() {
    return {
      showModal: false,
      tickets: [
      {
       name: 'alexey',
       email: 'alexey@mail.ru',
       mess: 'Неработает сайт',
       type_mess: 'Жалоба на сайт',
       priority: 'Высокий',
       status: 'В обработке',
       date: '11.02.2021, 16.11.57'
      },

      {
       name: 'philip',
       email: 'philip@mail.ru',
       mess: 'Неработает приложение',
       type_mess: 'Жалоба на приложение',
       priority: 'Высокий',
       status: 'Новый',
       date: '12.02.2021, 16.11.57'
      },

      ],
      };
  },

  methods: {
   addNewTicket(tick) {
    this.tickets.push(tick)
   },
   close() {
     this.$emit('close');
   },

  },

  components: {
    AllTickets,
    modal,
  },
}
</script>
