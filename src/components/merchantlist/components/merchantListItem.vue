<template>
    <article class="media">
        <div class="media-left">
            <figure class="image is-96x96">
                <img :src="merchant.logo">
            </figure>
        </div>
        <div class="media-content" style="font-size:12px">
            <strong>{{merchant.name}}</strong>
            <div class="level is-moblie">
                <div class="level-left">
                    <div>
                    <span v-for="item in getStars.starNum" :key="item" class="icon is-small  has-text-warning">
                        <i class="fas fa-star"></i>
                    </span>
                    <span v-for="item in getStars.halfStarNum" :key="'h'+item" class="icon is-small  has-text-warning">
                        <i class="fas fa-star-half"></i>
                    </span>
                    <span v-for="item in getStars.noStarNum" :key="'t'+item" class="icon is-small">
                        <i class="fas fa-star"></i>
                    </span>
                    <span>月售{{merchant.sales}}</span>
                </div>
                </div>
                <div class="level-right">
                    <span>{{merchant.deliveryTime}}min</span>|<span>{{formatDistance}}</span>
                </div>
            </div>
            <div class="level is-moblie">
                <div class="level-left">
                    <span>起送价 ￥{{merchant.minAmount}} </span>|<span>配送费 ￥{{formatDeliveryAmount}} </span>
                </div>
                <div class="level-right">
                    <span class="tag is-warning">美团专送</span>
                </div>
            </div>
            <div v-if="isSupportInvoice" class="level-moblie" style="margin-top:10px" >
                <div class="level-left">
                    <img class="image is-16x16" src="https://bulma.io/images/placeholders/128x128.png">
                    <span>本店支持开发票，开票金额{{formatInvoice}}起</span>
                </div>
            </div>
        </div>

    </article>
    
</template>

<script>
export default {
    name:"merchantListItem",
    props:["merchant"],
    data:function(){
        return{
            logo:"http://p0.meituan.net/waimaipoi/164f7baf5633038e3b81d72f287eaf685918.jpeg",
            name:"德克士",
            minAmount:200,
            isSupportInvoice:true,
            stars:3.5,
            sales:2772,
            distance:567,
            deliveryTime:30,
            deliveryAmount:200,
            meituanOnly:true,
            minInvoice:10000,
        } 
    },
    computed:{
        formatMinAmount:function(){
            return this.merchant.minAmount/100 +"元";
        },
        formatInvoice:function(){
            return this.merchant.minInvoice/100 +"元";
        },
        formatDeliveryAmount:function(){
            return this.merchant.deliveryAmount/100+"元";
        },
        formatDistance:function(){
            if(this.merchant.distance<1000){
                return this.merchant.distance + "m";
            }else{
                return this.merchant.distance/1000 + "km";
            }
        },
        getStars:function(){
            var starNum = parseInt(this.merchant.stars);
            var halfStarNum = Number.isInteger(this.merchant.stars)?0:1;
            var noStarNum = 5 - starNum - halfStarNum;
            return{
                starNum,halfStarNum,noStarNum
            }
        }
    },
   
};
</script>

<style scoped>
.level{
    margin:0px; 
    
}
.level-right{
    margin-top: 0px;
}
</style>
