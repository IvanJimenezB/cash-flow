<script setup>
    import { computed,defineProps, ref, defineEmits,toRefs, watch } from 'vue';


    const props= defineProps({amounts: Array})

    const {amounts} = toRefs(props)

    const points = computed(()=>{
        return amounts.value.reduce((acc,item,index)=>{
            const x = (300 / amounts.value.length) * (index + 1)
            let y = amountToPixels(item)
            return `${acc} ${x},${y} `
        },`0,${ amountToPixels(amounts.value.length != 0 ? amounts.value[0] : 0) } `)
    })

    const amountToPixels = (amount)=>{
        const min = Math.min(...amounts.value)
        const max = Math.max(...amounts.value)

        const amountAbs = amount + Math.abs(min)
        const minMax = Math.abs(max) + Math.abs(min)
        return 200 - ( (amountAbs * 100) / minMax) * 2
    }

    const zero = computed(()=> {
        return amounts.value.length == 0 ? 100 : amountToPixels(0)  
    })

    const showPointer = ref(false)

    const x = ref()

    watch(x,(value)=> {
        const index = Math.ceil((value / (300 / amounts.value.length)))
        if (index < 0 || index > amounts.value.length) return;
        emit('select', amounts.value[index - 1])
    })

    const emit = defineEmits(['select'])

    const tap = ({target, touches})=>{
        showPointer.value = true
        const elementWidth = target.getBoundingClientRect().width
        const elementX = target.getBoundingClientRect().x
        const touch = touches[0].clientX

        x.value = (touch - elementX) / elementWidth * 300
    }

    const untap = (e)=>{
        showPointer.value = false
    }

</script>
<template>
    <svg  
    @touchstart="tap"
    @touchmove="tap"
    @touchend="untap"
    viewBox="0 0 300 200" 
    >
        <line stroke="#c4c4c4" stroke-width="2" x1="0" :y1="zero" x2="300" :y2="zero" />
        <polyline fill="none" stroke="#0689B0" stroke-width="2" :points="points" />
        <line v-show="showPointer" stroke="#04b500" stroke-width="2" :x1="x" y1="0" :x2="x" y2="200" /> 
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