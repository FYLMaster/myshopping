<template>
	<div id="mpdd-house"><div class="mpdd-double-glist" avalonctrl="mpdd-house" style="visibility: visible;">
    <ul class="pd-goods-list">
        <li class="pd-glist-item" v-for="goods in goodslist">
            <div class="pd-goods-img">
                <img alt="goods"  v-bind:src="goods.hd_thumb_url">
            </div>
            <div class="pd-goods-txt">
                <span class="pd-goods-name">{{goods.goods_name}}</span>
                <span class="pd-goods-price">￥<span>{{goods.group.price/100}}</span></span>
                <span class="pd-goods-mprice">￥<span>{{goods.market_price/100}}</span></span>
            </div>
        </li>
    </ul>
</div></div>
</template>

<script type="text/javascript">
import bus from '../goods/eventBus'
    export default {
        data(){
            return {
                navindex:14,
                goodslist:''
            }
        },
    	created:function(){
            //this.navindex=this.$route.params.num;
            document.body.scrollTop = 0;
            var navid=this.navindex;
            console.log(navid)
            var that=this;
	        var url="/api/operation/"+navid+"/groups?opt_type=1&offset=0&size=50";
	        that.$http.get(url)
            .then(function(response){
                console.log(response.data.goods_list)
                that.goodslist=response.data.goods_list;
            },function(){
              alert("error")
            })
    	},
        mounted(){
            var that=this;
            bus.$on('listFun', function(data) {
                    that.goodslist = data;
                    console.log(that.goodslist)
            })
                 
        }
    }
</script>