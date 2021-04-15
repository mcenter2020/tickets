<template>
   <div>
    <table class="table table-striped table-sm">

    <tbody>
      <tr>
        <th class="w1" scope="row"><span class="badge badge-danger">#{{ index + 1}}</span><img src="@/assets/logo.png" alt="аватар не доступен" class="image-class"> {{ tick.name }}</th>

        <td class="w2"><h6><small class="text-muted">Тип обращения:&ensp;{{ tick.type_mess }}</small></h6><br>
        {{ tick.mess }}</td>
        <td class="w3"><span v-bind:class="{
           new: tick.status==='Новый',
           inwork: tick.status==='В обработке',
           later: tick.status==='Отложено',
           closed: tick.status==='Закрыто'
           }">
           </span><small class="text-muted">{{ tick.status }}</small></td>
        <td class="w4">{{ tick.priority }}</td>
        <td class="w5"><small class="text-muted">{{ tick.date }}</small></td>
      </tr>
    </tbody>
    </table><br><br>
    </div>
</template>


<script>
export default {
  props: {
    tick: {
     ticket: {
      type: Object,
      required: true
      },
    },
    index: Number
   }
  }
</script>

<style>


.image-class {
  height: 50px;
  width: 50px;
  margin-left: 30%;
}

.id-block {
  width: 10px;
}
.new {
  height: 15px;
  width: 15px;
  background-color: #a9d86e;
  border-radius: 50%;
  display: inline-block;
}

.inwork {
  height: 15px;
  width: 15px;
  background-color: #ff6c60;
  border-radius: 50%;
  display: inline-block;
}

.closed {
  height: 15px;
  width: 15px;
  background-color: #bec3c7;
  border-radius: 50%;
  display: inline-block;
}


.later {
  height: 15px;
  width: 15px;
  background-color: #fcb322;
  border-radius: 50%;
  display: inline-block;
}

.w1 {
  width: 30%;
}

.w2 {
   width: 40%;
 }

 .w3 {
   width: 10%;
 }

 .w4 {
   width: 10%;
 }

 .w5 {
   width: 10%;
 }

</style>
