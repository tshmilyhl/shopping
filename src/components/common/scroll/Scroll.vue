<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'
  export default {
    name: "Scroll",
    props:{
      probeType:{
        type:Number,
        default:0
      },
      pullUpLoad: {
        type:Boolean,
        default: false
      }
    },
    components:{
      BScroll
    },
    data(){
      return {
        scroll:null
      }
    },
    methods:{
      scrollTo(x,y,time){
        this.scroll&&this.scroll.scrollTo(x,y,time)
      },
      finishPullUp(){
        this.scroll&&this.scroll.finishPullUp()
      },
      refresh(){
         // console.log('---');
        this.scroll&&this.scroll.refresh()
      },
      getScrollY(){
        return this.scroll ? this.scroll.y:0
      }

    },
    mounted() {
      // this.$nextTick(()=>{
      //   this.scroll = new BScroll(this.$refs.wrapper,{
      //     scrollY:true,
      //     click:true,
      //     probeType:this.probeType,
      //     pullUpLoad:this.pullUpLoad
      //
      //   })
      // })
        //1.创建BScroll对象
      this.scroll = new BScroll(this.$refs.wrapper,{
        scrollY:true,
        click:true,
        probeType:this.probeType,
        pullUpLoad:this.pullUpLoad

      })
    //  2.监听滚动的位置
      if(this.probeType ===2 ||this.probeType ===3){
        this.scroll.on('scroll',position=>{
          // console.log(position)
          this.$emit('scroll',position)
        })
      }
      //监听scroll滚动到底部
      if(this.pullUpLoad){
        this.scroll.on('pullingUp',()=>{
          this.$emit('pullingUp')
        })
      }
    }
  }
</script>
<style scoped>
</style>
