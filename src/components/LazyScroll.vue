<script>
import axios from "axios"
export default {
    name:"LazyScroll",
    data(){
        return{
            posts:[],
            page:1,
            allowNewQuery:1
        }
    },
    mounted(){
    axios.get(`https://jsonplaceholder.typicode.com/posts?_page=${this.page}`)
    .then(res=>this.posts = res.data)
    },
    methods:{
        loadPosts(){
            if(this.$refs.container.scrollHeight === this.$refs.container.scrollTop + this.$refs.container.clientHeight || 0 === this.$refs.container.scrollTop){
            if(this.allowNewQuery == 1){
                new Promise((res,rej)=>{
                    this.allowNewQuery = 0
                    let a
                    if(this.$refs.container.scrollHeight === this.$refs.container.scrollTop + this.$refs.container.clientHeight){
                        a = this.page+1
                        axios.get(`https://jsonplaceholder.typicode.com/posts?_page=${a}`)
                        .then(res=>{
                            if(res.data.length > 0){
                                this.posts = res.data
                                this.page++
                                this.$refs.container.scrollTop = 255
                            }
                        })
                    }
                    if(0 === this.$refs.container.scrollTop){
                        a = this.page-1
                        axios.get(`https://jsonplaceholder.typicode.com/posts?_page=${a}`)
                        .then(res=>{
                            if(res.data.length > 0){
                                this.posts = res.data
                                this.page--
                                this.$refs.container.scrollTop = 255
                            }
                        })
                    }
                    res(1)
                }).then(res => this.allowNewQuery = res)
            }
            }
        }
    }
}
</script>

<template>
<div ref="container" id="lazyscroll" @scrollend="loadPosts">
    <div class="post" v-for="(post, index) in posts" >
        <span>@{{ post.userId }} | {{ post.title }}</span>
        <span>{{ post.body }}</span>
    </div>
</div>
</template>

<style scoped>
#lazyscroll{
    display: flex;
    width: 215px;
    height: 275px;
    flex-direction: column;
    gap: 5px;
    overflow-y: scroll;
    padding: 10px;
    box-sizing: border-box;
}
#lazyscroll::-webkit-scrollbar
.post{
    box-shadow: 3px 3px 3px gray;
    background-color: white;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    gap: 5px;
    width: 100%;
}
.post span:nth-child(1){
    font-weight: bold;
}
</style>