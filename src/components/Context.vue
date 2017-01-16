<template>
  <div class="body">
    <div class="page">
      <div @mouseenter="page.v_show.pageNumtop = true;
                        page.pageclass.top.pageEnter = true;"
           @mouseleave="
                        page.pageclass.top.pageEnter = false;" 
           class="top">
        <!-- <transition v-for="item in page.top" name="page-numshow">
          <span v-show="v_show.pageNumtop">{{item}}</span>
        </transition> -->
          <span v-for="item in page.num.top"
                v-show="page.v_show.pageNumtop"
                class="initial" 
                v-bind:class="page.pageclass.top"
                >{{item}}</span>
        <span>3</span>
      </div>
      <hr>
      <div  @mouseenter="page.v_show.pageNumbottom = true" 
            @mouseleave="page.v_show.pageNumbottom = false" 
            class="bottom">
        <transition v-for="item in page.num.bottom" name="page-numshow">
          <span v-show="page.v_show.pageNumbottom">{{item}}</span>
        </transition>
        
        <span>6</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Context',
  data () {
    return {
        page:{
          num:{
            bottom:[4,5,6,6],
            top:[1,2,3,3]
          },
          pageclass:{
            top:{
              'pageEnter':false,
              'pageLeave':false

            },
            bottom:{

            }
          },
          v_show:{
            pageNumbottom:false,
            pageNumtop:true
          }
        }
      
    }
  },
  methods:{
    
  },
  mounted(){
    
  },
  computed:{
    pageclass(){
      return 
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang = "less" scoped>
 /* .page-numshow-enter-active, .page-numshow-leave-active {
  transition: opacity .5s
}
.page-numshow-enter, .page-numshow-leave-to {
  opacity: 0;
}*/
  .body{
    height: 90%;
    width: 90%;
    border:1px solid #dedede;
    position: absolute;
    z-index: 0;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    .page{
      background-color: white;
      padding: 10px 0;
      width: 80px;
      position: absolute;
      top: 39%;
      left: 0px;
      transform: translate(-50%,0);
      hr{
        width: 20px;
        margin: 0 auto;
      }
      .top,.bottom{
        text-align: center;
        span{
          display: block;
          width: 20px;
          /*height: 32px;*/
          /*border:1px solid red;*/
          margin: 0 auto;
          line-height: 35px;
          color: #3c3463;
          /*background: red;*/
        }
        .initial{
          height: 0px;
          opacity: 0;
          transition: all 1s;
        }
        .pageEnter{
          height: 32px;
          opacity: 1;
        }
        .pageLeave{
          height: 0px;
          opacity: 0;
        }
      }
    }
  }

/*  .page-numshow-enter,.page-numshow-leave-to{
  height: 0px;
  opacity: 0;
}
.page-numshow-enter-to,.page-numshow-leave{
  height: 32px;
  opacity: 1;
}
.page-numshow-enter-active,.page-numshow-leave-active{
  transition: all .5s;
}*/
</style>
