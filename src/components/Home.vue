<script setup>
    import Layout from './Layout.vue'
    import Header from './Header.vue'
    import Resume from './Resume/Index.vue'
    import Movements from './Movements.vue'
</script>
<template>
    <Layout>
        <template #header>
            <Header/>
        </template>
        <template #resume>
            <Resume/>
        </template>
        <template #movements>
            <Movements/>
        </template>
    </Layout>
</template>