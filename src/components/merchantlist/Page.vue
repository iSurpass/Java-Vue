<template>
    <div>
        <merchantListNav :changeSort="changeSort"></merchantListNav>
        <merchantListItem v-for="item in page.data" :key="item.name" :merchant="item"></merchantListItem>
        <div class="has-text-centered" v-show="loadMoreing">
            正在加载...
        </div>
    </div>
    
</template>

<script>
import merchantListNav from "./components/merchantListNav.vue";
import merchantListItem from "./components/merchantListItem.vue";
import Vue from "vue";
export default {
    name:"MerchantList",
    data:function(){
        let data = [] ;
        for(let i=0;i<30;i++){
            data.push({
                logo:"http://p0.meituan.net/waimaipoi/164f7baf5633038e3b81d72f287eaf685918.jpeg",
                name:"第"+i+"家德克士",
                stars:4.5,
                sales:879+i,
                distance:568,
                minAmount:2000,
                deliveryAmount:200,
                meituanOnlu:true,
                isSupportInvoice:true,
                minInvoiceAmount:10000
            });
        }
        return{
            loadding:false,
            loadMoreing:true,
            data:data,
            page:{
                totalCount:0,
                totalPageNum:0,
                pageSize:10,
                pageNum:1,
                data:[]
            }
        };
    },
        mounted:function(){
            window.addEventListener("scroll",this.scrollFn);
        this.page.totalCount = this.data.length;
        let totalCount = this.page.totalCount;
        let temp = totalCount%this.page.pageSize;
        let pageNum = parseInt(totalCount/this.page.pageSize);
        if(temp>0){
            pageNum++;
        }else if(temp<0){
            pageNum = 1;
        }
        this.page.totalPageNum = pageNum;
        this.getPageData();
    },
            /*merchants:[{
                logo:"http://p0.meituan.net/waimaipoi/164f7baf5633038e3b81d72f287eaf685918.jpeg",
            name:"德克士",
            minAmount:2000,
            isSupportInvoice:true,
            stars:3.5,
            sales:2772,
            distance:567,
            deliveryTime:30,
            deliveryAmount:200,
            meituanOnly:true,
            minInvoice:10000,
            },{
                logo:"http://p0.meituan.net/120.0/waimaipoi/3fdb699b7997429ad021d1fccd61976a10046.jpg",
            name:"华莱士",
            minAmount:1000,
            isSupportInvoice:true,
            stars:4.5,
            sales:942,
            distance:8970,
            deliveryTime:30,
            deliveryAmount:200,
            meituanOnly:true,
            minInvoice:10000,
            },{
                logo:"http://p0.meituan.net/120.0/waimaipoi/3a34f9f5f8f0f9995a0eee7b90a0c06221994.jpg",
            name:"宝典八宝粥",
            minAmount:2000,
            isSupportInvoice:true,
            stars:2.5,
            sales:1092,
            distance:270,
            deliveryTime:50,
            deliveryAmount:200,
            meituanOnly:true,
            minInvoice:10000,
            }
            ]
        }*/
    methods:{
        nextPage:function(){
            if(this.page.pageNum===this.page.totalPageNum){
                this.loadMoreing = false;
                return;
            }
            if(this.loadding){
                return;
            }
            this.loadding=true;
            this.page.pageNum++;
            let scrollHeight = document.body.scrollHeight;
            setTimeout(()=>{
                this.getPageData();
                this.loadding = false;
                Vue.nextTick(function(){
                    document.documentElement.scrollTop = scrollHeight;
                });
            },1000)
        },
        scrollFn:function(){
            let pageHeight = Math.max(
                document.body.scrollHeight,
                document.body.offsetHeight
            );
            let viewportHeight =
            window.innerHeight||
            document.documentElement.clientHeight||
            document.body.clientHeight||
            0;
            let scrollHeight = 
            window.pageYOffset ||
            document.documentElement.scrollTop||
            document.body.scrollTop||
            0;
            let pos = pageHeight-viewportHeight-scrollHeight;
            if(pos<20){
                this.nextPage();
            }
        },
        getPageData:function(){
            let star = this.page.pageSize * (this.page.pageNum - 1);
            let end = star + this.page.pageSize;
            if(end>this.page.totalCount){
                end = this.page.totalCount;
            }
            const curData = this.data.slice(star,end);
            this.page.data = this.page.data.concat(curData);
        },
        /*nextPage:function(){
            this.page.nextPage++;
            let scrollHeight = document.body.scrollHeight;
            this.getPageData();
            Vue.nextTick(function(){
                document.documentElement.scrollTop = scrollHeight;
            });
        },*/
        changeSort:function(type){
            if(type===0){
                this.page.data.sort(function(a,b){
                    return a.sales-b.sales;
                });
            }else if(type===1){
                this.page.data.sort(function(a,b){
                    return b.sales-a.sales;
                });
            }
        }
    },
    components:{
        merchantListNav,merchantListItem
    }
}
</script>
