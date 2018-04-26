<template>
    <ul class="com-bottom" :style="{background:$store.state.bgColor}">
        <li><router-link to="/">电影</router-link></li>
        <li><router-link to="/MusicList">音乐</router-link></li>
        <li><router-link to="/BookList">书籍</router-link></li>
        <li><router-link to="/PhotoList">图片</router-link></li>        
    </ul>
</template>

<script>
    export default {
        
    }
</script>

<style scoped>
    .com-bottom{
        height: 1rem;
        background: rgb(33, 150, 243);
        position: fixed;
        bottom: 0;
        left: 0;
        width: 100%;
        display: flex;
    }
    .com-bottom li{
        flex-grow: 1;
        text-align: center;
        line-height: 1rem;
    }
    .com-bottom li a{
        color: #ccc;
        outline: none;
    }
    .com-bottom li a.router-link-exact-active{
        color: #fff;
    }
</style>