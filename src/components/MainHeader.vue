<template>
    <header class="header">
        <a href="">
            <img src="../assets/transpod_logo.png" height="30" width="80" alt="transpod">
        </a>
        <!-- <span>transpod</span> -->
    </header>
</template>

<script>
export default {
    name: 'MainHeader',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
    display: flex;
    justify-content: flex-start;
}
span {
    font-weight: bold;
    font-size: 20px;
}
</style>