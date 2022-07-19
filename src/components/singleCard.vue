<template>
    <div class="card mt-4">
        <img src="" class="card-img-top" alt="">
        <div class="my-card-body card-body">
            <p class="card-text">
                {{}}
            </p>
        </div>
    </div>
</template>

<script>
export default {
    props :{
        'element' : Object,
        'index' : Number,
    }
}
</script>

<style lang="scss" scoped> 
@import "../assets/style/variables.scss";

    .card{
        background-color: $backgroundHeader;
        border-radius: 0;
        p{
            color : $singersColor;
        }
    }
</style>