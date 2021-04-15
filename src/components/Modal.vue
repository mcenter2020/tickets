<template>
      <transition name="modal">

        <div class="modal-mask">
          <div class="modal-wrapper">
            <div class="modal-container">

              <div class="modal-header">
                <slot name="header">
                  default header
                </slot>
              </div>

              <div class="modal-body">
                <slot name="body">
                  <form @submit.prevent="onSubmit">
                  <div class="form-group">
                      <label for="InputName"><small class="text-muted">Имя:</small></label>
                      <input class="form-control" type="text" id="InputName" v-model="ticket.name">

                      <label for="InputEmail"><small class="text-muted">Email:</small></label>
                      <input class="form-control" type="text" id="InputEmail" v-model="ticket.email">

                      <label for="exampleFormControlTextarea1"><small class="text-muted">Сообщение:</small></label>
                      <textarea class="form-control" id="exampleFormControlTextarea1" rows="3" v-model="ticket.mess"></textarea>


                      <label for="FormControlSelect1"><small class="text-muted">Тип обращения:</small></label>
                      <select class="form-control" id="exampleFormControlSelect1" v-model="ticket.type_mess">
                        <option>Жалоба на пользователя</option>
                        <option>Жалоба на приложение</option>
                        <option>Жалоба на сайт</option>
                        <option>Оплата</option>
                        <option>Функционал</option>
                        <option>Авторизация</option>
                        <option>Модерация</option>
                        <option>Другое</option>
                     </select>



                   <label for="FormControlSelect2"><small class="text-muted">Приоритет:</small></label>
                   <select class="form-control" id="exampleFormControlSelect2" v-model="ticket.priority">
                     <option>Низкий</option>
                     <option>Средний</option>
                     <option>Высокий</option>
                     <option>Критический</option>
                   </select>


                   <label for="FormControlSelect3"><small class="text-muted">Статус:</small></label>
                   <select class="form-control" id="exampleFormControlSelect3" v-model="ticket.status">
                       <option v-bind:value="'В обработке'">В обработке</option>
                       <option v-bind:value="'Новый'">Новый</option>
                       <option v-bind:value="'Отложено'">Отложено</option>
                       <option v-bind:value="'Закрыто'">Закрыто</option>
                   </select><br>

                   <button class="b1" type='submit'>Создать</button>
                   <button class="b2" @click="$emit('close')">Отмена</button>
                   </div>

                   </form>
                </slot>
              </div>

              <div class="modal-footer">
                <slot name="footer">

                </slot>
              </div>
            </div>
          </div>
        </div>
      </transition>
</template>



<script>
  export default {
    name: 'modal',
    data() {
      return {
        showModal: true,
        ticket: {
          name: '',
          email: '',
          mess: '',
          type_mess: '',
          priority: '',
          status: null,
          date: ''
        },
       }
      },


    methods: {
      close() {
        this.$emit('close');
      },
      onSubmit() {
        console.log('Submit', this.ticket)
        if (this.ticket.name.trim()) {
         const newTicket = {
          date: new Date().toLocaleString(),
          name: this.ticket.name,
          email: this.ticket.email,
          mess: this.ticket.mess,
          type_mess: this.ticket.type_mess,
          priority: this.ticket.priority,
          status: this.ticket.status,
          status_text: this.ticket.status_text,
         }
         this.$emit('add-ticket', newTicket),
          this.ticket = {
          name: '',
          email: '',
          mess: '',
          type_mess: '',
          priority: '',
          status: 0,
          status_text: '',
          }
          this.$emit('close');
        }
        },
    },

  };
</script>


<style>
.modal-mask {
position: fixed;
z-index: 9998;
top: 0;
left: 0;
width: 100%;
height: 100%;
background-color: rgba(0, 0, 0, 0.5);
display: table;
transition: opacity 0.3s ease;
}

.modal-wrapper {
display: table-cell;
vertical-align: middle;
}

.modal-container {
width: 60%;
margin: 0px auto;
padding: 1px 3px;
background-color: #fff;
border-radius: 1%;
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
transition: all 0.3s ease;
font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
height: 12px;
margin-top: 0;
color: #bec3c7;
}

.modal-body {
margin: 1px 0;
}

.modal-default-button {
float: right;
}

/*
* The following styles are auto-applied to elements with
* transition="modal" when their visibility is toggled
* by Vue.js.
*
* You can easily play with the modal transition by editing
* these styles.
*/

.modal-enter {
opacity: 0;
}

.modal-leave-active {
opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
-webkit-transform: scale(1.1);
transform: scale(1.1);
}


.b1 {
    background: #78cd51;
    color: white;
    font-size: 9pt;
    border-radius: 8px;
    height:40px;
    width:90px;
    }

.b2 {
    background: #f67a6e;
    color: white;
    font-size: 9pt;
    border-radius: 8px;
    height:40px;
    width:90px;
    margin-left: 15px;
    }
</style>
