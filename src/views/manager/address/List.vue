<template>
    <div>
       <briup-fulllayout title="常用地址">
       <!-- {{info}} -->
          <van-list>
              <van-cell
                v-for="item in addresses"
                :key="item.id"
                :title="item.province+' '+item.city+' '+item.area+' '+item.address" 
                >            </van-cell>
          </van-list>
          <br>
         <van-button block type="primary" @click="toAddressEditHandler">
           添加
        </van-button>
          </briup-fulllayout>
    </div>
</template>

<script>

import {get,post}   from '../../../http/axios'
import {mapState} from 'vuex'
export default {
  computed:{  //计算属性
    //将状态机中的user对象中的info对象获取到
    ...mapState("user",["info"])
  },
    data() {
    return {
      addresses: [],
      
    };
  },
   created() {
        let id = this.info.id;
        this.loadAddress(id)
    },

  methods: {
 
    loadAddress(id){
       
        let url = '/address/findByCustomerId?id='+id
        get(url).then((response)=>{
        // push forEach silce {1,2,3,4,5,6,7} slice(0,6)
        this.addresses = response.data;
      })
    },


    toAddressEditHandler(){
      //跳转到页面处理函数
        this.$router.push("/manager/address_edit")
    }
  }
    
}
</script>