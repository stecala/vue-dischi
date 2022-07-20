<template>
    <div>
        <select class="form-select" aria-label="Default select example" v-model="authorSelect"
            @change="$emit('selectAuthor', authorSelect)">
            <option v-for="(element, index) in authorsList" :value="element" :key="index">{{element}}</option>
        </select>
    </div>
</template>

<script>
export default {
    data: function () {
        return {
            authorSelect: ''
        }
    },
     props : {
        authorsList : Array
    },
}
</script>

<style>
</style>