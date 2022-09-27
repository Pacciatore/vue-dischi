<template>
    <div>
        {{ errorMessage }}
    </div>
</template>

<script>
export default {
    name: 'ErrorMessageComponent',
    props: {
        errorMessage: String
    }
}
</script>

<style lang="scss" scoped>

</style>