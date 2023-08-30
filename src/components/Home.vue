<script setup>
    import Layout from './Layout.vue'
    import Header from './Header.vue'
    import Resume from './Resume/Index.vue'
    import Graphic from './Resume/Graphic.vue'
    import Action from './Action.vue'
    import Movements from './Movements/Index.vue'
    import { onMounted, reactive,ref, computed } from 'vue'

    let data = ref([])

    const amounts = computed(()=> { 
        return  data.value.filter(d => {
            const today = new Date()
            const oldDate = today.setDate(today.getDate() - 30)

            return d.time > oldDate
        }).map( m => m.amount)
    })
     
    const amount = ref(null)

    const select = (val)=> {
        amount.value = val
    }

    const save = (params)=> {
        const id = data.value !== null  ? 0 : data.value[data.value.length -1].id + 1 
        const form = {id,...params}
        data.value.push(form)
        saveStorage()
    }

    const deleteMovement = (id)=> {
        const index = data.value.findIndex(d => d.id === id)
        data.value.splice(index,1)
        saveStorage()
    }

    const saveStorage = ()=>{
        localStorage.setItem('data', JSON.stringify(data.value))
    }

    onMounted(()=>{
        const movements = JSON.parse(localStorage.getItem('data'))
        data.value = movements !== null ? movements.map(m => {
            return {...m,time: new Date(m.time)}    
        }) : [] 
    })
    const totalAmount = computed(()=>{
        return amounts.value.reduce((suma, movement ) => {
            return suma + movement
        },0)
    })

</script>
<template>
    <Layout>
        <template #header>
            <Header/>
        </template>
        <template #resume>
            <Resume :label="null" :amount="amount" :totalAmount="totalAmount">
                <template #graphic>
                    <Graphic :amounts="amounts" @select="select"/>
                </template>
                <template #action>
                    <Action @add="save" />
                </template>
            </Resume>
        </template>
        <template #movements>
            <Movements :movements="data" @delete="deleteMovement"/>
        </template>
    </Layout>
</template>