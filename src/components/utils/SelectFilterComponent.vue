<template>
    <div>

        <label for="genreSelection" class="pe-2 text-white">{{ filter.name }}:</label>

        <select name="genreSelection" id="genreSelection" class="col-4 rounded px-1 py-2" @change.prevent="doSearch">

            <option selected value="">All</option>

            <option v-for="element in filter.elements" :key="element" :value="element">
                {{ element }}
            </option>

        </select>

    </div>
</template>

<script>
export default {
    name: 'SelectFilterComponent',
    props: {
        filter: Object
    },
    methods: {
        doSearch(event) {
            this.$emit('search', event.target.value);
        }
    }

}
</script>

<style lang="scss" scoped>
@import '@/assets/style/variables.scss';

// Select genre element
#genreSelection {
    background-color: $tr-spotify-header;
    color: white;
    border-color: $tr-spotify-green;

    &:focus-visible {
        outline: none;
        background-color: $tr-spotify-main;
    }

}
</style>