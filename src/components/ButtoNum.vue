<script>
export default {
    name:"ButtoNum",
    props:{
        text:{
            type:String,
            required:true
        }
    },
    data(){
        return{

        }
    },
    methods:{
        clickYay(){
            console.log(this.text);
            this.$emit("clickYay", this.text)
        }
    }
}
</script>

<template>
<button @click="clickYay">{{ text }}</button>
</template>

<style scoped>
button{
    width: 50px;
    height: 50px;
    border: 0;
    box-shadow: 3px 3px 3px gray;
    background-color: white;
    border-radius: 10px;
    font-family: monospace;
}
</style>