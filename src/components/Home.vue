<script setup>
    import Layout from './Layout.vue'
    import Header from './Header.vue'
    import Resume from './Resume/Index.vue'
    import Action from './Action.vue'
    import Movements from './Movements/Index.vue'
    import { reactive } from 'vue'

    const data = [
        {id: 1,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:2500000},
        {id: 2,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:250000},
        {id: 3,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:250000},
        {id: 4,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-250000},
        {id: 5,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-250000},
        {id: 6,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:250000},
        {id: 7,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-250000},
        {id: 8,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:250000},
        {id: 9,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-250000},
        {id: 10,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:250000},
        {id: 11,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:250000},
        {id: 12,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-250000},
        {id: 13,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:250000},
        {id: 14,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:250000},
        {id: 15,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-250000},
        {id: 16,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:250000},
        {id: 17,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:250000},
        {id: 18,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:250000},
        {id: 19,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:250000},
    ]

    const movements = data.map((d)=> reactive(d))


</script>
<template>
    <Layout>
        <template #header>
            <Header/>
        </template>
        <template #resume>
            <Resume :label="null" :amount="null" :totalAmount="2000000">
                <template #graphic>
                    graphic
                </template>
                <template #action>
                    <Action/>
                </template>
            </Resume>
        </template>
        <template #movements>
            <Movements :movements="movements"/>
        </template>
    </Layout>
</template>