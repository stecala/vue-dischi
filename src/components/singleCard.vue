<template>
    <div class="card mt-4">
        <img :src="element.poster" class="card-img-top" alt="">
        <div class="my-card-body card-body text-center">
            <h5>{{element.title}}</h5> 
            <p >
                {{element.author}}<br>{{element.year}}
            </p>
        </div>
    </div>
</template>

<script>
export default {
    props :{
        'element' : Object,
    }
}
</script>

<style lang="scss" scoped> 
@import "../assets/style/variables.scss";

    .card{
        background-color: $backgroundHeader;
        border-radius: 0;
        padding: 25px  0;
        h5{
            color: $titleColor;
        }
        img{
            margin: 0 auto;
            width: 150px;
            height: 150px;
        }
        p{
            color : $singersColor;
        }
    }
</style>