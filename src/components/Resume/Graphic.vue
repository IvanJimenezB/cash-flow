<script setup>
    import { computed,defineProps } from 'vue';

    const props = defineProps({movements: Object})

    const amounts = props.movements.map((o)=> o.amount )

    const points = computed(()=>{
        return amounts.reduce((acc,item,index)=>{
            const x = index * 10
            let y = amountToPixels(item)
            return `${acc} ${x},${y} `
        },"")
    })

    const amountToPixels = (amount)=>{
        const min = Math.min(...amounts)
        const max = Math.max(...amounts)

        const amountAbs = amount + Math.abs(min)
        const minMax = Math.abs(max) + Math.abs(min)
        return 200 - ( (amountAbs * 100) / minMax) * 2
    }

    const zero = computed(()=> amountToPixels(0))

</script>
<template>
    <svg  viewBox="0 0 300 200">
        <line stroke="#c4c4c4" stroke-width="2" x1="0" :y1="zero" x2="300" :y2="zero" />
        <polyline fill="none" stroke="#0689B0" stroke-width="2" :points="points" />
        <line stroke="#04b500" stroke-width="2" x1="200" y1="0" x2="200" y2="200" />
    </svg>
    <p>Ultimos 30 días</p>
</template>
<style scoped>
svg {
  width: 100%;
}

p {
  text-align: center;
}
</style>