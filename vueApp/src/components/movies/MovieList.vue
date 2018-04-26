<template>
    <div class="movieList">
        <ul>
            <li v-for="(obj,index) in movies" :key="index" @click="fn(obj.id)">
                <div class="img-box">
                    <img :src="obj.img" alt="">
                </div>
                <div class="info-box">
                    <h2 class="title">{{obj.nm}}</h2>
                    <p>{{obj.ver}}</p>
                    <p>{{obj.star}}</p>
                    <p>{{obj.showInfo}}</p>                    
                </div>
            </li>
        </ul>
        <div class="load" v-show="isLoad">
            <img src="../../assets/images/loading.gif" alt="">
        </div>    
        <div class="end" v-show="isEnd">
            已经到底部了~~
        </div>   
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        data() {
            return {
                movies:[],
                isLoad: true,
                isEnd: false,
                flag: true
            }
        },
        methods:{
            load(){
                if(this.flag){
                    this.flag = false;
                    //axios 请求
                    axios.get(API_INTERFACE+'http://m.maoyan.com/movie/list.json?type=hot&offset=0'+this.movies.length+'&limit=10').then((res)=>{
                        if(res.data.data.movies<10){
                            this.isEnd = true;
                        }
                        this.movies = [...this.movies,...res.data.data.movies];
                        this.isLoad = false;
                        this.flag = true;                    
                        // console.log('请求成功');
                    }).catch(()=>{
                        console.log('请求失败');                
                    });
                }
            },
            fn(id){
                this.$router.push('/movieDetail/'+id)
            }
        },
        mounted:function(){
            //改变footer top 颜色 标题
            this.$store.commit('change',{bgColor:'rgb(33, 150, 243)',title:'Movie'});
            this.load();

            window.onscroll = () => {
                //已滑动高度
                var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
                //可视区高度
                var clientHeight = document.documentElement.clientHeight;
                //总高度
                var scrollHeight = document.documentElement.scrollHeight;
                if(scrollTop + clientHeight == scrollHeight){
                    if(!this.isEnd){
                        this.isLoad = true;
                        this.load();
                    }
                }
            }

        }
    }
</script>

<style scoped>
.movieList li{
    display: flex;
    padding: 0.2rem;
    border-bottom: 1px solid #ccc;
}
.img-box{
    flex-grow: 1;
    width: 0;
    margin-right: 0.2rem;
}
.img-box img{
    width: 100%;
}
.info-box{
    flex-grow: 2;
    width: 0;
}
.title{
    font-size: 0.33rem;
    font-weight: bold;
}
.info-box p{
    font-size: 0.27rem;
}
.load{
    text-align: center;
}
.end{
    text-align: center;
}
</style>