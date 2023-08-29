<script setup>
    import { ref, defineEmits, reactive } from "vue"
    import Modal from "./Modal.vue"

    const showModal = ref(false);

    const title = ref("");
    const amount = ref(0);
    const description = ref("");
    const movementType = ref();

    const emit = defineEmits(['add','delete'])

    const closeModal = () => {showModal.value = !showModal.value}

    const submit = () => {
      const form = reactive({
        title : title,
        description : description,
        amount : movementType.value === "Gasto" ? amount.value * -1 : amount ,
        time : new Date()
      })

      emit('add',form)
      title.value = ""
      amount.value = 0
      description.value = ""
      movementType.value = null
      closeModal()
    }

</script>
<template>
    <button @click="showModal = true">Agregar movimiento</button>
    <teleport to="#app">
        <Modal v-show="showModal" @closeModal="closeModal">
            <form action="#" @submit.prevent="submit">
                <div class="field">
                    <label for="title">Title</label>
                    <input type="text" id="title" v-model="title">
                </div>
                <div class="field">
                    <label for="amount">Amount</label>
                    <input type="number" id="amount" v-model="amount">
                </div>
                <div class="field">
                    <label for="description">Description</label>
                    <textarea id="descrition" cols="30" rows="3" v-model="description"></textarea>
                </div>
                <div class="field">
                    <label for="">Tipo de movimiento</label>
                    <label for="" class="radio-label"><input type="radio" v-model="movementType" value="Ingreso"> <span>Ingreso</span></label>
                    <label for="" class="radio-label"><input type="radio" v-model="movementType" value="Gasto"> <span>Gasto</span></label>
                </div>

                <div class="action">
                    <button>Agregar movimiento</button>
                </div>
            </form>
        </Modal>
    </teleport>
</template>
<style scoped>
button {
  color: white;
  font-size: 1.25rem;
  background-color: var(--brand-blue);
  border: none;
  width: 100%;
  padding: 24px 60px;
  border-radius: 60px;
  box-sizing: border-box;
}

form {
  font-size: 1.24rem;
  width: 100%;
}

form .action {
  padding: 0 24px;
}

.field {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  padding: 16px 24px;
}

label {
  margin-bottom: 8px;
}

input,
textarea {
  font-size: 1.24rem;
  border: 2px solid var(--brand-blue);
  border-radius: 8px;
  padding: 8px;
}

input[type="number"] {
  text-align: right;
}

.radio-label {
  display: flex;
  align-items: center;
  margin-top: 8px;
}

.radio-label span {
  margin-top: 4px;
  margin-left: 8px;
}

input[type="radio"] {
  appearance: none;
  width: 1.24rem;
  height: 1.24rem;
  color: var(--brand-blue);
  border: 2px solid var(--brand-blue);
  border-radius: 50%;
}

input[type="radio"]:checked {
  background-color: var(--brand-blue);
}
</style>