<template>
    <briup-fulllayout title="常用地址">
        <van-list>
            <van-cell
                v-for="item in address"
                :key="item.id"
                :title="item.province+' '+item.city+' '+item.area+' '+item.address">
            </van-cell>
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
        return{
            address:[]
        }
    },
    created(){
        this.loadAddress();

    },
    computed:{//计算属性
    //将状态机中的
        ...mapState("user",["info"])
    },
    methods:{
        loadAddress(){
            let id=this.info.id;
            let url="/address/findByCustomerId?id="+id
            get(url).then((Response)=>{
                this.address=Response.data;
            })
        },
        //跳转到地址编辑页面的处理函数
        toAddressEditHandler(){
            //跳转
            this.$router.push("/manager/address_edit");
        }

    }
    
}
</script>