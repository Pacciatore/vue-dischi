<template>
    <div class="text-center col-2 p-3 d-flex flex-column justify-content-start">

        <div class="img-container">
            <img class="img-fluid" :src="info.poster" :alt="info.title">
        </div>

        <h4 class="text-white fw-bold text-uppercase py-3"> {{ info.title }}</h4>
        <div class="disk-author">
            {{ info.author }}
            <p>
                {{ info.year }}
            </p>

        </div>

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
@import '@/assets/style/variables.scss';

div.d-flex {
    background-color: $tr-spotify-header;

    .img-container {
        min-height: 183px;
        color: white;
    }

    .disk-author {
        color: #808080;
    }

    transition: box-shadow 0.15s;

    &:hover {
        box-shadow: inset 0px 0 10px 5px white;
        cursor: pointer;
    }

}
</style>