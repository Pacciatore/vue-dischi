<template>
    <main class="py-5">

        <DiskListComponent :disksInfo="disksInfo" />

    </main>
</template>

<script>
import DiskListComponent from "@/components/utils/DiskListComponent.vue";

export default {
    name: "MainComponent",
    props: {
        disksInfo: Array
    },
    components: { DiskListComponent }
}
</script>

<style lang="scss" scoped>
@import '@/assets/style/variables.scss';

main {
    background-color: $tr-spotify-main;
}
</style>