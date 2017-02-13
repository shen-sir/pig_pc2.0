<template>
  <div class="body">
    <div class="context">
      <div class="left">
        <img class="large" src="../assets/daquan.png" >
        <img class="small" src="../assets/xiaoquan.png" >
        <img class="apple" src="../assets/apple.png" >
        <h1>&nbsp&nbsp&nbsp&nbsp苹果客户端下载</h1>
        <small>APPLE CLIENT DOWNLOAD</small>
      </div>
      <div class="right">
        <img class="large" src="../assets/daquan.png" >
        <img class="small" src="../assets/xiaoquan.png" >
        <img class="apple" src="../assets/android.png" >
        <h1>&nbsp&nbsp&nbsp&nbsp安卓客户端下载</h1>
        <small>ANDROID CLIENT DOWNLOAD</small>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Finally',
  data () {
    return {
      
    }
  },
  methods:{
    
  },
  mounted(){
    // console.log(this.show)
  },
  computed:{
   
  },
  watch:{
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang = "less" scoped>
  @keyframes an{
  0%{
    transform: rotate(0deg);
    -webkit-transform: rotate(0deg);
    -ms-transform: rotate(0deg);
    -o-transform: rotate(0deg);
  }
    100%{
      transform: rotate(720deg);
      -webkit-transform: rotate(720deg);
      -ms-transform: rotate(720deg);
      -o-transform: rotate(720deg);
    }
}
@-webkit-keyframes an{
  0%{
    transform: rotate(0deg);
    -webkit-transform: rotate(0deg);
    -ms-transform: rotate(0deg);
    -o-transform: rotate(0deg);
  }
    100%{
      transform: rotate(720deg);
      -webkit-transform: rotate(720deg);
      -ms-transform: rotate(720deg);
      -o-transform: rotate(720deg);
    }
}
@keyframes anb{
  0%{
    transform: rotate(0deg);
    -webkit-transform: rotate(0deg);
    -ms-transform: rotate(0deg);
    -o-transform: rotate(0deg);
  }
  100%{
    transform: rotate(-720deg);
    -webkit-transform: rotate(-720deg);
    -ms-transform: rotate(-720deg);
    -o-transform: rotate(-720deg);
  }
}
@-webkit-keyframes anb{
  0%{
    transform: rotate(0deg);
    -webkit-transform: rotate(0deg);
    -ms-transform: rotate(0deg);
    -o-transform: rotate(0deg);
  }
  100%{
    transform: rotate(-720deg);
    -webkit-transform: rotate(-720deg);
    -ms-transform: rotate(-720deg);
    -o-transform: rotate(-720deg);
  }
}

  .body{
    height: 100%;
    background-image: url("../assets/finally.png");
    background-size: cover;
    background-position: center; 
    .context{
      height: 90%;
      width: 90%;
      min-width: 920px;
      border: 1px solid #dedede;
      position: absolute;
      z-index: 0;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      -webkit-transform: translate(-50%, -50%);
      -ms-transform: translate(-50%, -50%);
      -o-transform: translate(-50%, -50%);
      .left{
        /*border: 1px solid red;*/
        display: inline-block;
        position: absolute;
        top: 47%;
        left: 30%;
        transform: translate(-50%, -50%);
        -webkit-transform: translate(-50%, -50%);
        -ms-transform: translate(-50%, -50%);
        -o-transform: translate(-50%, -50%);
        text-align: center;
        img{
          position: absolute;
          left: 50px;
          /*transform: translate(-50%, 0);*/
          margin: 0 auto;
        }
        .large{
          /*animation:animations3 2s linear infinite;*/
          animation: an 20s infinite;
          -o-animation: an 20s infinite;
          -webkit-animation:an 20s infinite;
        }
        .small{ 
          animation: anb 20s infinite; 
          -webkit-animation:anb 20s infinite;
          -o-animation: anb 20s infinite;
        }
        .apple{
          margin: 28px ;
        }
        h1{
          color: white;
          margin-top: 210px;
          font-size: 34px;
          background: url(../assets/applelogo.png) no-repeat;
          background-position: 6px 4px;
          background-size: 30px;
        }
        small{
          color: #b57dea;
          font-size: 14.16666px;
        }
      }
      .right {
        /*border: 1px solid red;*/
        display: inline-block;
        position: absolute;
        top: 47%;
        right: 0%;
        transform: translate(-50%, -50%);
        -webkit-transform: translate(-50%, -50%);
        -ms-transform: translate(-50%, -50%);
        -o-transform: translate(-50%, -50%);
        text-align: center;
        img{
          position: absolute;
          left: 50px;
          margin: 0 auto;
        }
        .large{
          animation: anb 20s infinite;
          -webkit-animation: anb 20s infinite;
          -o-animation: anb 20s infinite;
        }
        .small{
           animation: an 20s infinite ;
           -webkit-animation: an 20s infinite;
           -o-animation: an 20s infinite;
        }
        .apple{
          margin: 28px ;
        }
        h1{
          color: white;
          margin-top: 210px;
          font-size: 34px;
          background: url(../assets/androidlogo.png) no-repeat;
          background-position: 6px 4px;
          background-size: 30px;
        }
        small{
          color: #b57dea;
          font-size: 14.16666px;
        }
      }
    }
  }

</style>
