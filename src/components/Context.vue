<template>
  <div class="body">
    <div class="title" >
      <!-- 这里的span标签动画没有生效，控制台中看不到过渡的class属性 -->
      <span v-bind:class="content.class">{{content.context.title}}</span>
    </div>
    <div class="page">
      <div @mouseenter="page.pageclass.top.pageEnter = true;"
           @mouseleave="page.pageclass.top.pageEnter = false;" 
           class="top">
          <span v-for="item in page.num.top"
                class="initial" 
                v-bind:class="page.pageclass.top"
                >{{item}} <strong>啊</strong>
                </span>
          <span>3</span>
      </div>
      <div @mouseenter="page.pageclass.bottom.pageEnter = true;"
           @mouseleave="page.pageclass.bottom.pageEnter = false;" 
            class="bottom">
          <span v-for="item in page.num.bottom"
                class="initial"
                v-bind:class="page.pageclass.bottom">{{item}}<strong>啊</strong></span>
        <span>6</span>
      </div>
    </div>
    <div class="left-content">
      <div class="hid-h1" >
      <!-- 改这里，动画生效的地方，没有加enter只是在测试 -->
        <!-- <h1 @mouseenter="content.class.transleave=true"
            @mouseleave="content.class.transleave=false"
            @transitionend="trans"
            v-bind:class="content.class">{{content.context.h1}}</h1> -->
        <h1 @transitionend="trans"
            v-bind:class="content.class">{{content.context.h1}}</h1>
      </div>
      <div class="hid-small">
        <small v-bind:class="content.class">{{content.context.small}}</small>
      </div>
      <div class="line" v-bind:class="content.class"></div>
      <div class="text">
        <p v-bind:class="content.class" v-html="content.context.text"></p>
      </div>
    </div>
    <h1>000{{message}}</h1>
    <img class="right-content" v-bind:class="content.class" :src="content.context.imgUrl">
    <div class="oh">
      <div class="botton" v-bind:class="content.class"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Context',
  props:['message'],
  data () {
    return {
        // parent:this.message,
        page:{
          num:{
            bottom:[4,5,6,6],
            top:[1,2,3,3],
            // text:
          },
          pageclass:{
            top:{
              'pageEnter':false,
              'pageLeave':false

            },
            bottom:{
              'pageEnter':false,
              'pageLeave':false
            }
          }
        },
        content:{
          class:{
              'transleave':false,
              'transenter':false
          },
          context:{
              title:'title',
              h1:'猪队友开黑房间',
              small:'zhu dui you kaihei',
              text:'独特的开黑房间包括了语音，视频，文字三种交流方式<br>独特的开黑房间包括了语音，视频，文字三种交流方式',
              imgUrl:'../static/img/diyiping-tu.png',
              color:''
          }
            
        },
        textData:[
          {
            title:'title0',
            h1:'猪队友开黑房间001',
            small:'zhu dui you kaihei0',
            text:'独特的开黑房间包括了语音，视频，文字三种交流方式<br>独特的开黑房间包括了语音，视频，文字三种交流方式',
            imgUrl:'../static/img/diyiping-tu.png',
            color:''
          },
          {
            title:'title0',
            h1:'猪队友开黑房间002',
            small:'zhu dui you kaihei0',
            text:'独特的开黑房间包括了语音，视频，文字三种交流方式<br>独特的开黑房间包括了语音，视频，文字三种交流方式',
            imgUrl:'../static/img/diyiping-tu.png',
            color:''
          },
          {
            title:'title0',
            h1:'猪队友开黑房间003',
            small:'zhu dui you kaihei0',
            text:'独特的开黑房间包括了语音，视频，文字三种交流方式<br>独特的开黑房间包括了语音，视频，文字三种交流方式',
            imgUrl:'../static/img/diyiping-tu.png',
            color:''
          },
          {
            title:'title0',
            h1:'猪队友开黑房间004',
            small:'zhu dui you kaihei0',
            text:'独特的开黑房间包括了语音，视频，文字三种交流方式<br>独特的开黑房间包括了语音，视频，文字三种交流方式',
            imgUrl:'../static/img/diyiping-tu.png',
            color:''
          },
          {
            title:'title0',
            h1:'猪队友开黑房间005',
            small:'zhu dui you kaihei0',
            text:'独特的开黑房间包括了语音，视频，文字三种交流方式<br>独特的开黑房间包括了语音，视频，文字三种交流方式',
            imgUrl:'../static/img/diyiping-tu.png',
            color:''
          },
          {
            title:'title0',
            h1:'猪队友开黑房间006',
            small:'zhu dui you kaihei0',
            text:'独特的开黑房间包括了语音，视频，文字三种交流方式<br>独特的开黑房间包括了语音，视频，文字三种交流方式',
            imgUrl:'../static/img/diyiping-tu.png',
            color:''
          }
        ]
      
    }
  },
  methods:{
    trans(){
      // console.log(this.message)
      this.content.context = this.textData[this.message-1];
      this.content.class.transleave=false;
    }
  },
  mounted(){
    // console.log(this.show)
  },
  computed:{
    pageclass(){
      return 
    }
  },
  watch:{
    message(val, oldVal){
      console.log(val+'=='+oldVal)
      if(val>1){
        this.content.class.transleave=true;
      }
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang = "less" scoped>
  .body{
    height: 90%;
    width: 90%;
    min-width: 920px;
    border:1px solid #dedede;
    position: absolute;
    z-index: 0;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    .title{
      position: absolute;
      height: 0.23rem;
      top: -0.1rem;
      left: 0.3rem;
      background: white;
      padding: 0 0.1rem;
      overflow-y: hidden;
      span{
        display: inline-block;
        transition: all 1s;
      }
      .transleave{
        margin-top:.3rem;
      }
    }
    .page{
      background-color: white;
      padding: 0.1rem 0;
      width: 0.8rem;
      font-size: 20px;
      hr{
        width: 0.2rem;
        margin: 0 auto;
      }
      .top,.bottom{
        text-align: center;
        background: white;
        span{
          display: block;
          width: 0.2rem;
          margin: 0 auto;
          line-height: 0.35rem;
          color: #3c3463;
          overflow:hidden; 
          position: relative;
          strong{
            display: inline-block;
            position: absolute;
            background-color: white;
            opacity: 0;
            transform: translate(-100%,100%);
            transition: all .5s;
          }
        }
        span:hover>strong{
            opacity: 1;
            transform: translate(-100%,0%);
        }
        .initial{
          height: 0.0rem;
          opacity: 0;
          transition: all 1s;
        }
        .pageEnter{
          height: 0.32rem;
          opacity: 1;
        }
        .pageLeave{
          height: 0.0rem;
          opacity: 0;
        }
      }
      .top{
        position: absolute;
        bottom: 50%;
        left: 0%;
        transform: translate(-50%,0);
      }
      .bottom{
        border-top: 1px solid black;
        position: absolute;
        top: 50%;
        left: 0.0rem;
        transform: translate(-50%,0);
      }
    }
    .left-content{
      width: 3.9rem;
      position: absolute;
      top: 36.7%;
      left: 25%;
      transform: translate(-50%,0);
      .hid-h1{
        height: 0.40rem;
        overflow-y:hidden;
      }
      .hid-small{
        height: 0.33rem;
        margin-bottom: 0.2rem;
        overflow-y:hidden;
      }
      h1{
        font-size: 0.32rem;
        margin-bottom: -0.15rem;
        color: #7e5fa0;
        opacity: 1;
        transition: all 1s;
      }
      .transleave{
        /*opacity: 0;*/
        transform: translate3d(0,0.8rem,0);
      }
      .transenter{
        /*opacity: 1;*/
        transform: translate3d(0,0px,0);
      }
      small{
        display: inline-block;
        font-size: 0.2rem;
        color: #9d65b2;
        opacity: 1;
        transition: all 1s;
      }
      .line{
        height: 0.04rem;
        width: 0.82rem;
        background-color: #551e85;
        transition: all 1s;
      }
      .line.transleave{
        width: 0;
        transform: translate3d(0,0px,0);
      }
      .text{
        margin-left: 1.0rem;
        margin-top: -0.13rem;
        font-size: 0.15rem;
        line-height: 0.2rem;
        color: #a4abb5;
        opacity: 1;
        overflow-y: hidden;
        p{
          transition: all 1s;
        }
      }
    }
    .oh{
      width: 2.22rem;
      height: 0.38rem;
      overflow-y: hidden;
      background-color: white;
      position: absolute;
      bottom: -0.4rem;
      left: 50%;
      transform: translate(-50%,-50%);
      .botton{
        width: 1.22rem;
        height: 0.36rem;
        border:1px solid black;
        background-color: red;
        margin: 0 auto;
        transition: all 1s;
      }
      .botton.transleave{
        margin-top: 0.5rem;
      }
    }
    
    .right-content{
      width: 4rem;
      position: absolute;
      top: 50%;
      right: 0;
      transform: translate(0,-50%);
      transition: all 1s;
    }
    .right-content.transleave{
      opacity: 0;
      transform: translate(80%,-50%);
    }
  }

</style>
