<template>
    <main>

        <div class="container d-flex flex-wrap gap-5">
            <DiskComponent v-for="disk in diskInfo" :key="disk.title" :info="disk" />
        </div>

    </main>
</template>

<script>
import DiskComponent from './DiskComponent.vue';

export default {
    name: "DiskListComponent",
    props: {
        diskInfo: Array
    },
    components: {
        DiskComponent
    }
}
</script>

<style lang="scss" scoped>

</style>