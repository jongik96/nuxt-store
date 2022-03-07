<template>
  <div>
      <h1>메인 페이지</h1>
      <p>메인 페이지입니다</p>
  </div>
</template>

<script>
// import axios from 'axios';
export default {
  // async created(){
  //   console.log('test')
  //   try{
  //     const response = await axios.get('http://localhost:3000/products');
  //     console.log('axios 호출');
  //     console.log(response);
  //   }catch(error){
  //     console.log(error);
  //   }
  // }
    // async created() {
    //   const response = await this.$axios.get("http://localhost:3000/products");
    //   console.log(response);
    // },
    async asyncData({$axios}){
      const response = await $axios.get('http://localhost:3000/products');
      console.log(response);
    }
}
</script>

<style>

</style>