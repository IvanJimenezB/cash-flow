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
            <Resume :label="null" :amount="null" :totalAmount="2000000">
                <template #graphic>
                    graphic
                </template>
                <template #action>
                    action
                </template>
            </Resume>
        </template>
        <template #movements>
            <Movements/>
        </template>
    </Layout>
</template>