<script setup>
import {computed, defineProps, toRefs} from "vue"

const props = defineProps({
    label: {type: String, default: "Ahorro Total"},
    totalAmount: Number,
    amount: {type:Number,default : null},
})

const {amount} = toRefs(props)

const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric'}
const date = new Date().toLocaleDateString("es-CO",options)

const currencyFormat = new Intl.NumberFormat("es-CO",{style: "currency",currency:"COP",maximumFractionDigits:0})

const visualAmount = computed(()=> currencyFormat.format((amount.value !== null ? amount.value : props.totalAmount))) 

const label  = computed(()=> props.label !== null ? props.label : date )

</script>
<template>
    <main>
        <p>{{ label }}</p>
        <h1>{{ visualAmount }}</h1>
        <div class="graphic">
            <slot name="graphic"></slot>
        </div>
        <div class="action">  
            <slot name="action"></slot>
        </div>
    </main>
</template>
<style scoped>

main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}

h1,
p {
  margin: 0;
  text-align: center;
}

h1 {
  margin-top: 14px;
  color: var(--brand-green);
}
.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
  flex-direction: column;
}
</style>