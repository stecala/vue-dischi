<template>
    <div>
        <select class="form-select" aria-label="Default select example" v-model="userSelect" @change="$emit('select' , userSelect)">
            <option value="Rock" >Rock</option>
            <option value="Pop" >Pop</option>
            <option value="Jazz" >Jazz</option>
            <option value="Metal" >Metal</option>
            <option value="" >All Genre</option>
        </select>
    </div>
</template>

<script>
export default {
    data : function(){
        return{
            userSelect : ''
        }
    }
}
</script>

<style lang="scss" scoped>
</style>