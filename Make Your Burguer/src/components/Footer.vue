<template>
    <footer id="footer">
        <p>Make Your Burger &COPY; 2022</p>
    </footer>
</template>

<script>
export default {
    name: 'Footer',
}
</script>

<style scoped>
    #footer{
        height: 200px;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: #222;
        border-top: 4px solid #111;
        color:  #fcba03;
    }
</style>