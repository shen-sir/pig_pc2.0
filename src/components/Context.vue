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
                @click="pagetrans"
                >{{item}} <strong>啊</strong>
                </span>
          <span v-bind:class="content.class">{{page.inpage}}</span>
      </div>
      <div @mouseenter="page.pageclass.bottom.pageEnter = true;"
           @mouseleave="page.pageclass.bottom.pageEnter = false;" 
            class="bottom">
          <span v-for="item in page.num.bottom"
                class="initial"
                v-bind:class="page.pageclass.bottom"
                @click="pagetrans"
                >{{item}}<strong>啊</strong></span>
        <span>5</span>
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
    <!-- <h1>000{{message}}</h1> -->
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
            top:[1],
            bottom:[2,3,4,5],
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
          },
          inpage:1
        },
        content:{
          class:{
              'transleave':false,
              'transenter':false
          },
          context:{
            title:'PIGGYMATE',
            h1:'猪队友·主页',
            small:'PIGGYMATE HOME',
            text:'"猪队友"是一款多功能社交开黑平台。玩家可以在右上角个人中心包装自己添加。<br>个性标签，上线匹配开黑队友或直接多人开黑。<br>点击小猪上线与好友一起享受开黑乐趣吧。',
            imgUrl:'../static/img/diyiping-tu.png',
            color:''
          }
            
        },
        textData:[
          {
            title:'PIGGYMATE',
            h1:'猪队友·主页',
            small:'PIGGYMATE HOME',
            text:'"猪队友"是一款多功能社交开黑平台。玩家可以在右上角个人中心包装自己添加。<br>个性标签，上线匹配开黑队友或直接多人开黑。<br>点击小猪上线与好友一起享受开黑乐趣吧。',
            imgUrl:'../static/img/diyiping-tu.png',
            color:''
          },
          {
            title:'PIGGYMATE',
            h1:'猪队友·开黑房间',
            small:'PIGGYMATE BLACK ROOM',
            text:'独特的开黑房间包括了语音，视频，文字三种交流方式。<br>房间中不仅包括了拉人踢人查看个人信息这些基础功能。',
            imgUrl:'../static/img/dierping-tu.png',
            color:''
          },
          {
            title:'PIGGYMATE',
            h1:'猪队友·陪玩',
            small:'PIGGYMATE PLAY',
            text:'一个人玩游戏是不是有些寂寞？<br>四缺一是不是有些无奈说不出？<br>找些志同道合的人一起开黑吧！',
            imgUrl:'../static/img/disanping-tu.png',
            color:''
          },
          {
            title:'PIGGYMATE',
            h1:'猪队友·认证',
            small:'PIGGYMATE IDENTIFICATUON',
            text:'妹子/大神在上传完认证资料后，我们会在第一时间由后台人工审核。<br>审核成功后会有独特的认证标志并且可以成为陪玩自由定价开始接单啦。',
            imgUrl:'../static/img/disiping-tu.png',
            color:''
          }
        ]
      
    }
  },
  methods:{
    trans(){

      this.content.context = this.textData[this.thismessage];
      
      if (this.message>this.page.inpage) {
        // alert(this.message-this.page.inpage+'向下')
        for(let i=0;i <this.message-this.page.inpage;i++){
          // alert('循环')
          this.page.num.top.push(this.message-i);
          this.page.num.bottom.shift()
        }
      }else if(this.message<this.page.inpage){
        // alert(this.page.inpage-this.message)
        for(let i=0;i <this.page.inpage-this.message;i++){
          // alert('循环')
          this.page.num.bottom.unshift(this.message+i+1);
          this.page.num.top.pop();
        }
        
      }
      this.page.num.bottom.sort();
      this.page.num.top.sort();
      this.page.inpage = this.message;
      this.content.class.transleave=false;
    },
    pagetrans(e){
      // console.log(Number(e.currentTarget.childNodes[0].nodeValue) )
      this.$emit('pagetrans',Number(e.currentTarget.childNodes[0].nodeValue))
    }
  },
  mounted(){
  },
  computed:{
    thismessage(){
      if(this.message-1<0){
        return 0
      }else if(this.message-1>3){
        return 3
      }
      return this.message-1
    }
  },
  watch:{
    thismessage(val, oldVal){
      console.log(val+'=='+oldVal)
      this.content.class.transleave=true;
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
    -ms-transform: translate(-50%,-50%);
    -o-transform: translate(-50%,-50%);
    -webkit-transform: translate(-50%,-50%);
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
        -o-transition: all 1s;
        -webkit-transition: all 1s;
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
        span:nth-last-of-type(2){
          height: 0rem;
          opacity: 0;
        }
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
            -webkit-transform: translate(-100%,100%);
            -ms-transform: translate(-100%,100%);
            -o-transform: translate(-100%,100%);
            transition: all .5s;
            -webkit-transition: all .5s;
            -o-transition: all .5s;
            
          }
        }
        span:hover>strong{
            opacity: 1;
            transform: translate(-100%,0%);
            -webkit-transform: translate(-100%,0%);
            -ms-transform: translate(-100%,0%);
            -o-transform: translate(-100%,0%);
        }
        .initial{
          height: 0.0rem;
          opacity: 0;
          transition: all 1s;
          -webkit-transition: all 1s;
          -o-transition: all 1s;
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
        overflow-x: hidden;
        transform: translate(-50%,0);
        -ms-transform: translate(-50%,0);
        -o-transform: translate(-50%,0);
        -webkit-transform: translate(-50%,0);
        .transleave{
          transform: translate(-20px,0);
          -webkit-transform: translate(-20px,0);
          -ms-transform: translate(-20px,0);
          -o-transform: translate(-20px,0);
          transition: all 1s;
          -webkit-transition: all 1s;
          -o-transition: all 1s;
        }
      }
      .bottom{
        border-top: 1px solid black;
        position: absolute;
        top: 50%;
        left: 0.0rem;
        transform: translate(-50%,0);
        -webkit-transform: translate(-50%,0);
        -ms-transform: translate(-50%,0);
        -o-transform: translate(-50%,0);
      }
    }
    .left-content{
      width: 3.9rem;
      position: absolute;
      top: 36.7%;
      left: 25%;
      transform:  translate(-50%,0);
      -webkit-transform:  translate(-50%,0);
      -ms-transform:  translate(-50%,0);
      -o-transform:  translate(-50%,0);
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
        transition:  all 1s;
        -webkit-transition:  all 1s;
        -o-transition:  all 1s;
      }
      .transleave{
        transform: translate3d(0,0.8rem,0);
        -webkit-transform: translate3d(0,0.8rem,0);
        -ms-transform: translate3d(0,0.8rem,0);
        -o-transform: translate3d(0,0.8rem,0);
      }
      .transenter{
        transform: translate3d(0,0px,0);
        -webkit-transform: translate3d(0,0px,0);
        -ms-transform: translate3d(0,0px,0);
        -o-transform: translate3d(0,0px,0);
      }
      small{
        display: inline-block;
        font-size: 0.15rem;
        color: #9d65b2;
        opacity: 1;
        transition: all 1s;
        -webkit-transition: all 1s;
        -o-transition: all 1s;
      }
      .line{
        height: 0.04rem;
        width: 0.82rem;
        background-color: #551e85;
        transition: all 1s;
        -webkit-transition: all 1s;
        -o-transition: all 1s;
      }
      .line.transleave{
        width: 0;
        transform: translate3d(0,0px,0);
        -webkit-transform: translate3d(0,0px,0);
        -ms-transform: translate3d(0,0px,0);
        -o-transform: translate3d(0,0px,0);
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
          -webkit-transition: all 1s;
          -o-transition: all 1s;
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
      -webkit-transform: translate(-50%,-50%);
      -ms-transform: translate(-50%,-50%);
      -o-transform: translate(-50%,-50%);
      .botton{
        width: 1.22rem;
        max-width: 140px;
        height: 0.36rem;
        max-height: 41px;
        border:1px solid red;
        margin: 0 auto;
        transition: all 1s;
        -webkit-transition: all 1s;
        -o-transition: all 1s;
      }
      .botton.transleave{
        margin-top: 0.5rem;
      }
    }
    
    .right-content{
      width: 4rem;
      max-width: 420px;
      position: absolute;
      top: 50%;
      right: 0;
      transform: translate(0,-50%);
      -webkit-transform: translate(0,-50%);
      -ms-transform: translate(0,-50%);
      -o-transform: translate(0,-50%);
      transition: all 1s;
      -webkit-transition: all 1s;
      -o-transition: all 1s;
    }
    .right-content.transleave{
      opacity: 0;
      transform: translate(80%,-50%);
      -webkit-transform: translate(80%,-50%);
      -ms-transform: translate(80%,-50%);
      -o-transform: translate(80%,-50%);
    }
  }

</style>
