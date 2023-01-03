<template>
    <div id="main-banner">
        <h1>MAKE YOUR BURGER</h1>
    </div>
</template>

<script>
    export default {
        name: 'Banner'
    }
</script>

<style scoped>
    #main-banner{
        height: 500px;
        background-image: url('../../public/img/burger.jpg');
        background-position: 0 -250px;
        background-size: cover;
        background-repeat: no-repeat;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }
    #main-banner h1{
        color:#fcba03;
        text-align: center;
        font-size: 7vh;
        background-color: #222;
        padding: 20px 40px;
    }
</style>