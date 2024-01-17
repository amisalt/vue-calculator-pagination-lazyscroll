<script>
import Calculator from "./components/Calculator.vue"
import Pagination from "./components/Pagination.vue";
import LazyScroll from "./components/LazyScroll.vue";
export default {
  name:"App",
  components:{Calculator,Pagination,LazyScroll},
  data(){
    return {
    }
  }
}
</script>

<template>
<Calculator></Calculator>
<Pagination></Pagination>
<LazyScroll></LazyScroll>
</template>

<style scoped>

</style>
