<template>
  <div>
    <nav-bar>
        <div slot="left" class="back" @click="backClick">
          <img src="~assets/img/common/back.svg" alt="">
        </div>
      <div slot="center" class="title">
        <div v-for="(item,index) in titles"
             class="title-item"
             :class="{active:currentIndex===index}"
             @click="titleClick(index)">
          {{item}}
        </div >
      </div>

    </nav-bar>
  </div>
</template>

<script>
  import NavBar from "components/common/navbar/NavBar";
  export default {
    name: "DetailNavBar",
    components:{
      NavBar
    },
    data(){
      return {
        titles:['商品','参数','评论','推荐'],
        currentIndex:0
      }
    },
    methods:{
      backClick(){
        this.$router.back()
      },
      titleClick(index){
        this.currentIndex=index
        this.$emit('titleClick',index)
      }
    }
  }
</script>

<style scoped>
  .title{
    display:flex;
    font-size: 14px;
    flex-direction: row;
  }
  .title-item{
    flex: 1;
  }
  .active{
    color: var(--color-high-text)
  }
  .back img {
    margin-top: 12px;
  }
</style>
