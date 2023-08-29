<script setup>
    import { defineProps, toRefs } from 'vue';
    const props = defineProps({movement: Object})
    // const movement = toRefs(props.movement)

    const format = new Intl.NumberFormat("es-CO",{style: "currency", currency: "COP",maximumFractionDigits:0})
    const amountFormat = format.format(props.movement.amount)
    
    const emit = defineEmits(['remove'])

    const remove = ()=> {
        emit("remove",props.movement.id)
    }


</script>
<template>
    <div class="movement">
       <div class="content">
            <h4>{{ movement.title }}</h4>
            <p>{{ movement.description }}</p>
       </div>
       <div class="action">
            <img src="../../assets/trash-icon.svg" alt="Trash icon" @click="remove">
            <h4 :class="{red:movement.amount < 0,green:movement.amount>=0}">{{ amountFormat }}</h4>
       </div>
    </div>
</template>
<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}
.movement .content {
  width: 100%;
}
.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}
h4,
p {
  margin: 0;
  padding: 0;
}
h4 {
  margin-bottom: 8px;
}
.movement .action img {
  margin-bottom: 16px;
}
.red {
    color: red;
}
.green {
    color: green;
}
</style>