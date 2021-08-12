<template>
    <div data-aos="flip-up" data-aos-duration="700" class="container">
        <h1>Welcome :)</h1>
        <h1>Do you want to try it for free ?</h1>
        <button class="btn btn-success mt-4"><a @click="RTGA">Try for free</a></button>
    </div>
</template>
<script>
export default{
    methods : {
        RTGA(){
            this.$emit("CP", "app-ag");
        }
    }
}
</script>
<style scoped>
    h1{
        font-size:25px;
        color:white;
        font-family: "Nunito", sans-serif;
    }
    h1:first-child{
        margin-top: 4em;
    }
    button a{
        color:black;
        text-decoration: none;
        font-weight: bold;
        font-family: "Nunito", sans-serif;
        cursor: pointer;
    }
</style>
