<template>
  <div class="home">
    <header class="header">
      <!-- 头部图片 -->
      <img src="../../assets/home.jpg" alt="">
    </header>
    <!-- 内容区域 6 -->
          <van-grid :column-num="3">
        <van-grid-item
          v-for="value in categories"
          :key="value.id"
          :icon="value.icon"
          :text="value.name"
        />
        <!-- 产品区域 n -->
      </van-grid>
       <van-grid :column-num="1" icon-size="400px">
        <briup-product-item
          @click="toBuyHandler(value)"
          v-for="value in products"
          :key="value.id"
          :data="value"
        >
        </briup-product-item>
      </van-grid>
    <!-- 产品区域 n -->
   
  </div>
</template>
<script>
import {get,post}   from '../../http/axios'
export default {
  data() {
    return {
      categories:[],
      products:[]
    }
  },
  
  created(){
    this.loadCategories();
    this.loadProducts();
  },
  methods:{
    //加载栏目信息
    loadCategories(){
      let url = '/category/findAll'
      get(url).then((response)=>{
        // push forEach silce {1,2,3,4,5,6,7} slice(0,6)
        this.categories = response.data.slice(0,6);
      })
    },
    loadProducts(){
      let url = '/product/query'
      let params = {
        page:0,
        pageSize:10
      }
      post(url,params).then((response)=>{
        this.products = response.data.list;
      })
    },
    toBuyHandler(p){
      this.$router.push({
        path:"/manager/order_confirm",
        query:p
      })
      
    }

  }
}
</script>
<style scoped>
.home {
  padding-bottom: 50px;
}
.header {
  height: 300px;
  overflow: hidden;
}
.header img {
  width: 100%;
}
</style>