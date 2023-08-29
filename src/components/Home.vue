<script setup>
    import Layout from './Layout.vue'
    import Header from './Header.vue'
    import Resume from './Resume/Index.vue'
    import Graphic from './Resume/Graphic.vue'
    import Action from './Action.vue'
    import Movements from './Movements/Index.vue'
    import { reactive,ref } from 'vue'

    const data = ref([
        {id: 1,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:0, time: new Date('2023-08-1')},
        {id: 2,title: "para eliminar",description:"esto es una descripcion de ejemplo xd xd",amount:2, time: new Date('2023-08-2')},
        {id: 3,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:25, time: new Date('2023-08-3')},
        {id: 4,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-25, time: new Date('2023-08-4')},
        {id: 5,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-25, time: new Date('2023-08-5')},
        {id: 6,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:30, time: new Date('2023-08-6')},
        {id: 7,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:0, time: new Date('2023-08-7')},
        {id: 8,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:25, time: new Date('2023-08-8')},
        {id: 9,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-10, time: new Date('2023-08-9')},
        {id: 10,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:10, time: new Date('2023-08-10')},
        {id: 11,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:2, time: new Date('2023-08-11')},
        {id: 12,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-1, time: new Date('2023-08-12')},
        {id: 13,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:3, time: new Date('2023-08-13')},
        {id: 14,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:5, time: new Date('2023-08-14')},
        {id: 15,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:7, time: new Date('2023-08-15')},
        {id: 16,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:8, time: new Date('2023-08-16')},
        {id: 17,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:23, time: new Date('2023-08-17')},
        {id: 18,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:12, time: new Date('2023-08-18')},
        {id: 19,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:22, time: new Date('2023-08-19')}
    ])

    // const movements = data.map((d)=> reactive(d))
    const amounts = data.value.filter(d => {
        const today = new Date()
        const oldDate = today.setDate(today.getDate() - 30)

        return d.time > oldDate
    }).map( m => m.amount)
    
    const am = amounts.map((m,i)=> {
        const lastMovements = amounts.slice(0,i)
        return lastMovements.reduce((suma, movement ) => {
            return suma + movement
        },0)
    })

    const select = ()=> {
        alert('hace select')
    }

    const save = (params)=> {
        const id = data.value[data.value.length -1].id + 1
        const form = {id,...params}
        data.value.push(form)
    }

    const deleteMovement = (id)=> {
        const index = data.value.findIndex(d => d.id === id)
        data.value.splice(index,1)
    }

</script>
<template>
    <Layout>
        <template #header>
            <Header/>
        </template>
        <template #resume>
            <Resume :label="null" :amount="null" :totalAmount="2000000">
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