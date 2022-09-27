<template>
    <div class="text-center col-3 d-flex flex-column">
        <div class="img-container">
            <img :src="info.poster" :alt="info.title">
        </div>

        <h2> {{ info.title }}</h2>
        <p>
            {{ info.author }}
        </p>
        <p>
            {{ info.year }}
        </p>
    </div>
</template>

<script>
export default {
    name: 'DiskComponent',
    props: {
        info: Object
    }
}
</script>

<style lang="scss" scoped>

</style>