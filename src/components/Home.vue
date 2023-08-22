<script setup>
    import Layout from './Layout.vue'
    import Header from './Header.vue'
    import Resume from './Resume/Index.vue'
    import Graphic from './Resume/Graphic.vue'
    import Action from './Action.vue'
    import Movements from './Movements/Index.vue'
    import { reactive } from 'vue'

    const data = [
        {id: 1,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:0},
        {id: 2,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:2},
        {id: 3,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:25},
        {id: 4,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-25},
        {id: 5,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-25},
        {id: 6,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:30},
        {id: 7,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:0},
        {id: 8,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:25},
        {id: 9,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-10},
        {id: 10,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:10},
        {id: 11,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:2},
        {id: 12,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:-1},
        {id: 13,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:3},
        {id: 14,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:5},
        {id: 15,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:7},
        {id: 16,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:8},
        {id: 17,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:23},
        {id: 18,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:12},
        {id: 19,title: "Ahorro",description:"esto es una descripcion de ejemplo xd xd",amount:22},
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
                    <Graphic :movements="movements"/>
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