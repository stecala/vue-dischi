<template>
    <div class="card mt-4">
        <img src="" class="card-img-top" alt="">
        <div class="my-card-body card-body">
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's
                content.</p>
        </div>
    </div>
</template>

<script>
export default {

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