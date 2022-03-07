<template>
  <div class="app">
    <main>
       <!-- :search-keyword="searchKeyword"
       @input="updateSearchKeyword" -->
      
      <SearchInput

        v-model="searchKeyword"
       @search="searchProducts"
       ></SearchInput>
      <ul>
        <li
         v-for="product in products" :key="product.id"
          class="item flex"
          @click="moveToDetailPage(product.id)"
        >
          <!-- {{product}} -->
          <img class="product-image" :src="product.imageUrl" :alt="product.name">
          <p>{{product.name}}</p>
          <span>{{product.price}}</span>
        </li>
      </ul>
    </main>
  </div>
</template>

<script>
import axios from 'axios';
import { fetchProductByKeyword } from '~/api';

export default {
  async asyncData(){
      const res = await axios.get('http://localhost:3000/products');
      const products = res.data.map(item =>({
        ...item,
        imageUrl: `${item.imageUrl}?random=${Math.random()}`
      }));
      // const products = res.data.map((item) =>{
      //   return{
      //     ...item,
      //     imageUrl: `${item.imageUrl}?random=${Math.random()}`
      //   }
      // })
      return {products};
  },

  data(){
    return{
      searchKeyword: '',
    }
  },
  methods:{
    moveToDetailPage(id){
      console.log(id);
      this.$router.push(`detail/${id}`);
    },

    // 하위 컴포넌트에서 받아온 값
    // updateSearchKeyword(keyword){
    //   this.searchKeyword = keyword;
    // },


    async searchProducts(){
      const response = await fetchProductByKeyword(this.searchKeyword);
      // console.log(response.data);
      this.products = response.data.map(item =>({
        ...item,
        imageUrl: `${item.imageUrl}?random=${Math.random()}`
      }));
    }
  },
  // data(){
  //   return{
  //     products: [],
  //   }
  // },
  // async created(){
  //   const response = await axios.get('http://localhost:3000/products');
  //   console.log(response);
  //   this.products = response.data;
  // }


}
</script>

<style scoped>
.flex {
  display: flex;
  justify-content: center;
}
.item {
  display: inline-block;
  width: 400px;
  height: 300px;
  text-align: center;
  margin: 0 0.5rem;
  cursor: pointer;
}
.product-image {
  width: 400px;
  height: 250px;
}
.app {
  position: relative;
}
.cart-wrapper {
  position: sticky;
  float: right;
  bottom: 50px;
  right: 50px;
}
.cart-wrapper .btn {
  display: inline-block;
  height: 40px;
  font-size: 1rem;
  font-weight: 500;
}
</style>