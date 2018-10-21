<template>
    <div class="waimai-dropdown" :style="getShow">
        <div class="level is-mobile" @click="changeSort(0)">
            <span class="level-left">综合排序</span>
        </div>
        <hr class="dropdown-divider">
        <div class="level is-mobile" @click="changeSort(1)">
            <span class="level-left">销量排序</span>
        </div>
    </div>
</template>

<script>
export default {
    name:"SortDropdown",
    props:["isShow","changeSort"],
     computed:{
        getShow:function(){
            if(this.isShow){
                return "display:block";
            }else{
                return "display:none";
            }
        }
    },
}
</script>
<style scoped>
.waimai-dropdown{
position: absolute;
width: 100%;
z-index: 22;
background-color: white;
}
.level{
    margin: 8px;
}
</style>
