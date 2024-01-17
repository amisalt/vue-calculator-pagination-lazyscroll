<script>
import axios from "axios"
export default {
    name:"Pagination",
    data(){
        return{
            posts:[],
            page:1,
        }
    },
    mounted(){
    axios.get(`https://jsonplaceholder.typicode.com/posts?_page=${this.page}`)
    .then(res=>this.posts = res.data)
    },
    methods:{
        leftButton(){
            if(this.page > 1){
                this.page--
                axios.get(`https://jsonplaceholder.typicode.com/posts?_page=${this.page}`)
                .then(res=>{
                    if(res.data.length > 0){
                        this.posts = res.data
                    }
                })
            }
            
        },
        rightButton(){
            let a = this.page+1
            axios.get(`https://jsonplaceholder.typicode.com/posts?_page=${a}`)
            .then(res=>{
                if(res.data.length > 0){
                    this.posts = res.data
                    this.page++
                }
            })
        }
    }
}
</script>

<template>
<div id="pagination">
    <div id="nav">
        <button @click="leftButton">←</button>
        <span>{{ page }}</span>
        <button @click="rightButton">→</button>
    </div>
    <div id="posts">
        <div class="post" v-for="(post, index) in posts" >
            <span>@{{ post.userId }} | {{ post.title }}</span>
            <span>{{ post.body }}</span>
        </div>
    </div>
</div>
</template>

<style scoped>
#pagination{
    width: 235px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 10px;
}
#nav{
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
}
#posts{
    display: flex;
    width: 100%;
    height: 248px;
    flex-direction: column;
    gap: 5px;
    overflow-y: scroll;
    padding: 10px;
    box-sizing: border-box;
}
button{
    background-color: transparent;
    font-family: monospace;
    box-shadow: none;
    border: 0;
}
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