<template>
  <div id="app">
    
    <transition name="fade" >
      <hello v-show="show.show_1"></hello>
    </transition>
    <Context ></Context>
  </div>
</template>

<script>
import Hello from './components/Hello'
import Context from './components/Context'

export default {
  name: 'app',
  data(){
    return{
      show:{
        // 改初始化
        // show_1:true,
        show_1:false,
        show_2:false,
        show_3:false,
        show_4:false,
        show_5:false,
        show_6:false
      },
      scrollNem:0
    }
  },
  components: {
    Hello,
    Context
  },
  methods:{
    addEvent:(function(window, undefined) {        
        var _eventCompat = function(event) {
            var type = event.type;
            if (type == 'DOMMouseScroll' || type == 'mousewheel') {
                event.delta = (event.wheelDelta) ? event.wheelDelta / 120 : -(event.detail || 0) / 3;
            }
            //alert(event.delta);
            if (event.srcElement && !event.target) {
                event.target = event.srcElement;    
            }
            if (!event.preventDefault && event.returnValue !== undefined) {
                event.preventDefault = function() {
                    event.returnValue = false;
                };
            }
            /* 
               ......其他一些兼容性处理 */
            return event;
        };
        if (window.addEventListener) {
            return function(el, type, fn, capture) {
                if (type === "mousewheel" && document.mozHidden !== undefined) {
                    type = "DOMMouseScroll";
                }
                el.addEventListener(type, function(event) {
                    fn.call(this, _eventCompat(event));
                }, capture || false);
            }
        } else if (window.attachEvent) {
            return function(el, type, fn, capture) {
                el.attachEvent("on" + type, function(event) {
                    event = event || window.event;
                    fn.call(el, _eventCompat(event));    
                });
            }
        }
        return function() {};    
    })(window),
    start(){
      // alert(0)
      for(let i=0;i<this.show.length;i++){
        this.show['show_'+this.scrollNem] = false;
      }
      if (this.scrollNem == 0) {
        this.show['show_1'] = true;
      }else{
        this.show['show_1'] = false;
      }
    },
  },
  mounted(){
    let that = this;
    this.addEvent(document.body,"mousewheel",function(event) {
        if (event.delta < 0) {
          // that.show = false;
          that.scrollNem += 1
          // console.log("鼠标向上滚了！");
          console.log(that.scrollNem)
        }else{
          // that.show = true;
          that.scrollNem -= 1
          // console.log('向下')
          console.log(that.scrollNem)
        }
        that.start()
    })
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
}
html,body{
  width: 100%;
  height: 100%;
}
html{
  overflow: hidden;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  /*抗锯齿属性*/
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #2c3e50;
  /*margin-top: 60px;*/
  width: 100%;
  min-width: 1020px;
  height: 100%;
  /*border:1px solid black;*/
  overflow:hidden;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0;
}
</style>
