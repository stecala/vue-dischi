<template>
    <div>
        <select class="form-select" aria-label="Default select example" v-model="userSelect" @change="$emit('select' , userSelect)">
            <option v-for="(element, index) in genresList" :value="element" :key="index">{{element}}</option>
            <option value="" >All Genres</option>
        </select>
    </div>
</template>

<script>

export default {
    data : function(){
        return{
            userSelect : ''
        }
    },
    props : {
        genresList : Array
    },
}
</script>

<style lang="scss" scoped>
</style>