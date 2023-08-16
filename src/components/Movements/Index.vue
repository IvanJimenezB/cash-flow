<script setup>
    import { defineProps, toRefs} from "vue"
    import Movement from "./Movement.vue"
    const props = defineProps({movements: Array})

    const {movements} = toRefs(props)

    const remove = (id)=>{
      alert("Emitido" + id)
    }

</script>
<template>
    <div class="movements">
        <h2 class="title">Historial</h2>
        <div class="content">
          <Movement v-for="movement in movements" :key="movement.id" :movement="movement" @remove="remove" />
        </div>
    </div>
</template> 
<style scoped>
.movements {
  max-height: 100%;
  padding: 0 8px;
  margin-bottom: 14px;
}
.title {
  margin: 8px 16px 24px 16px;
  color: var(--brand-blue);
}
.content {
  max-height: 68vh;
  display: flex;
  flex-direction: column;
  gap: 8px;
  overflow-y: scroll;
}
</style>