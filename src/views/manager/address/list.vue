<template>
  <briup-fulllayout title="常用地址">
    <!-- {{addresses}} -->
    <!-- {{info}} -->
    <van-list>
      <van-cell v-for="item in addresses" 
        :key="item.id"
        :title="item.province+' '+item.city+' '+item.area+' '+item.address"
        />
    </van-list>
    <br>
    <van-button block type="default" @click="toAddressEditHandler">添加</van-button>
  </briup-fulllayout>
</template>

<script>
import {get} from '../../../http/axios'
import {mapState} from 'vuex'
export default {
  data(){
    return {
      addresses:[]
    }
  },
  computed:{  // 计算属性
    // 将状态机中的user对象中的info对象获取到
    ...mapState("user",["info"])
  },
  created(){
    // 调用加载地址信息的方法
    this.loadAddress();
  },
  methods:{
    // 加载当前顾客地址信息
    loadAddress(){
      let id = this.info.id;  // 假装当前用户id为26
      let url = "/address/findByCustomerId?id="+id;
      get(url).then((response)=>{
        this.addresses = response.data;
      })
    },
    // 跳转到地址编辑页面的处理函数
    toAddressEditHandler(){
      // 编程跳转
      this.$router.push("/manager/address_edit");
    },
  }
}
</script>