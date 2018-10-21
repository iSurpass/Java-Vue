<template>
   <div>
        <nav class="level is-moblie">
            <div class="level-item has-text-centered">
                <div class="level-item">
                    <span class="nav-title">美食</span>
                    <span class="icon">
                        <i class="fas fa-angle-down"/>
                    </span>
                </div>
                <div class="level-right">|</div>
            </div>
            <div class="level-item has-text-centered">
                <div class="level-item" @click="openSort(true)">
                    <span class="nav-title">综合排序</span>
                    <span class="icon">
                        <i class="fas fa-angle-down"/>
                    </span>
                </div>
                <div class="level-right">|</div>
            </div>
            <div class="level-item has-text-centered">
                <div class="level-item">
                    <span class="nav-title">筛选</span>
                    <span class="icon">
                        <i class="fas fa-filter"/>
                    </span>
                </div>
                
            </div>
        </nav>
        <Sort :isShow="isSortShow" :changeSort="callbackChangeSort"></Sort>
        <div class="shadow" @click="openSort(false)" :style="getShow"></div>
        <div class="tabs">
            <ul></ul>
        </div>
        
    </div>
</template>

<script>
import Sort from "./SortDropdown.vue";
export default {
    name:"merchantListNav",
    props:["changeSort"],
    data:function(){
        return{
            isSortShow:false
        }
    },
    computed:{
        getShow:function(){
            if(this.isSortShow){
                return "display:block";
            }else{
                return "display:none";
            }
        }
    },
    methods:{
        openSort(isOpen){
            this.isSortShow=isOpen;
        },
        callbackChangeSort:function(type){
            this.changeSort(type);
            this.isSortShow=false;
        }
    },
    components:{
        Sort
    }
}
</script>

<style scoped>
    .level{
        margin: 10px;
    }
    .nav-title{
        font-size: 13px;
    }
    .icon{
        font-size: 12px;
    }
    .shadow{
        position: absolute;
        top: 180px;
        left: 0px;
        right: 0px;
        bottom: 0px;
        z-index: 19;
        background:rgba(0, 0, 0, 0.5)
    }
</style>

