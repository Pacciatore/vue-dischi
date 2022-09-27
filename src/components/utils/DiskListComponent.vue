<template>
    <main>

        <div class="container d-flex flex-wrap gap-5">
            <DiskComponent v-for="disk in disksInfo" :key="disk.title" :info="disk" />
        </div>

    </main>
</template>

<script>
import DiskComponent from './DiskComponent.vue';

export default {
    name: "DiskListComponent",
    props: {
        disksInfo: Array
    },
    components: {
        DiskComponent
    }
}
</script>

<style lang="scss" scoped>

</style>