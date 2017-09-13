<template>
    <div class="subject-nav-wrapper">
        <ul class="subject-nav-list">
            <li class="subject-nav-item" v-for="(item,index) in items" :class="{'cur-subject-nav-item': item.active}" @click='navbtn(item.id,index)'>
                <span>{{item.name}}</span>
            </li>           
        </ul>
        <div class="subject-nav-btn">
            <img src="//mcdn.pinduoduo.com/assets/img/mpdd_cat_arrow.png">
        </div>
        <div class="subject-nav-gradient"></div>
    </div>
</template>

<script type="text/javascript">
import bus from '../goods/eventBus'
    export default {
        data(){
            return {
                items:[
                    {name:'服饰箱包', id:14, active:true},
                    {name:'当季女鞋', id:18, active:false},
                    {name:'品牌男装', id:1135, active:false},
                    {name:'家居百货', id:15, active:false},
                    {name:'环球美食', id:1, active:false},
                    {name:'数码家电', id:18, active:false},
                    {name:'家纺家具', id:818, active:false},
                    {name:'水果生鲜', id:13, active:false},
                    {name:'母婴呵护', id:4, active:false},
                    {name:'全球海淘', id:12, active:false},
                    {name:'美妆护肤', id:16, active:false},
                    {name:'运动户外', id:43, active:false}
                ]
            }
        },
        methods:{
            navbtn:function(navid,index){
                console.log(navid)
                for(var i=0; i<this.items.length;i++){
                    this.items[i].active = false;
                }
                this.items[index].active = true;
                var that=this;
                var url="/api/operation/"+navid+"/groups?opt_type=1&offset=0&size=50";
                that.$http.get(url)
                .then(function(response){
                    console.log(response.data.goods_list)
                    bus.$emit("listFun",response.data.goods_list)
                },function(){
                  alert("error")
                })
            }
        }
    }
</script>