<template>
    <div class="searchbar-container">
        <input type="text" class="searchbar" 
        v-model="searchVal" 
        @keyup.enter.native="submitSearch" 
        placeholder="Search by name..">
    </div>
</template>

<script>
import EventBus from '../App.vue'

export default {
    props: ['searchStudentByName'],
    data() {
        return {
            searchVal: '',
        }
    },
    methods: {
        submitSearch() {
            this.searchInput = ''
            this.$emit('searchInputChanged', this.searchVal)
        }
    },
    beforeMount () {
        this.searchVal = this.findStudentByName
    },
    watch: {
        searchVal() {
            this.$emit('searchInputChanged', this.searchVal)
        }
    }
}
</script>

<style scoped>
    .searchbar-container {
        width: 100%;
        text-align: center;
        margin-top: 10px;
    }

    .searchbar {
        width: 93%;
        font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
        font-size: 18px;
        padding: 10px;
        border: none;
        color: gray;
        -moz-appearance: none;
        -webkit-appearance: none;
        outline-color: none;
        border-bottom: 1px solid lightgray;
        transition: all 0.2s;
    }
    
    .searchbar:active, .searchbar:focus {
        -moz-appearance: none;
        outline-width: 0;
        -webkit-appearance: none;
        outline-color: none;
        border-bottom: 2px solid black;
    }

</style>
