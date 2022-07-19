<template>
    <header>
        <div class="logo-container">
            <a href="">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/19/Spotify_logo_without_text.svg/2048px-Spotify_logo_without_text.svg.png"
                alt="spotify logo">
            </a>
        </div>
    </header>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
@import "../assets/style/variables.scss";

.logo-container {
    background-color: $backgroundHeader;

    img {
        width: 40px;
        height: 40px;
        margin: 15px;
    }
}
</style>