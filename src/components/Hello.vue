<template>
  <div class="body">
  <canvas height="620" width="1360" id="canvas" style=" height: 100%;"/>
  <div class="text">
    <h1>猪队友</h1>
    <h1>P I G G Y M A G E</h1>
  </div>
  </div>
</template>

<script>
window.canvasObj={
        canvasEl :null,
        ctx : null,
        mousePos : [0, 0],

        easingFactor : 5.0,
        backgroundColor : '#000',
        nodeColor : '#fff',
        edgeColor : '#fff',
        nodes : [],
        edges : []
      }
export default {
  name: 'hello',
  // props:[''],
  data () {
    return {
      windowSize:window.innerWidth/window.innerHeight,
      
    }
  },
  methods:{
    constructNodes() {
      let that = this;
      for (var i = 0; i < 50; i++) {
        var node = {
          drivenByMouse: i == 0,
          x: Math.random() * window.canvasObj.canvasEl.width,
          y: Math.random() * window.canvasObj.canvasEl.height,
          vx: Math.random() * 1 - 0.5,
          vy: Math.random() * 1 - 0.5,
          radius: Math.random() > 0.9 ? 3 + Math.random() * 3 : 1 + Math.random() * 3
        };

        window.canvasObj.nodes.push(node);
      }

      window.canvasObj.nodes.forEach(function (e) {
        window.canvasObj.nodes.forEach(function (e2) {
          if (e == e2) {
            return;
          }

          var edge = {
            from: e,
            to: e2
          }

          that.addEdge(edge);
        });
      });
    },
    addEdge(edge) {
      var ignore = false;

      window.canvasObj.edges.forEach(function (e) {
        if (e.from == edge.from && e.to == edge.to) {
          ignore = true;
        }

        if (e.to == edge.from && e.from == edge.to) {
          ignore = true;
        }
      });

      if (!ignore) {
        window.canvasObj.edges.push(edge);
      }
    },
    step() {
      let that = this;
      window.canvasObj.nodes.forEach(function (e) {
        if (e.drivenByMouse) {
          return;
        }

        e.x += e.vx;
        e.y += e.vy;

        function clamp(min, max, value) {
          if (value > max) {
            return max;
          } else if (value < min) {
            return min;
          } else {
            return value;
          }
        }

        if (e.x <= 0 || e.x >= window.canvasObj.canvasEl.width) {
          e.vx *= -1;
          e.x = clamp(0, window.canvasObj.canvasEl.width, e.x)
        }

        if (e.y <= 0 || e.y >= window.canvasObj.canvasEl.height) {
          e.vy *= -1;
          e.y = clamp(0, window.canvasObj.canvasEl.height, e.y)
        }
      });

      this.adjustNodeDrivenByMouse();
      this.render();
      window.requestAnimationFrame(this.step);
    },
    adjustNodeDrivenByMouse() {
      window.canvasObj.nodes[0].x += (window.canvasObj.mousePos[0] - window.canvasObj.nodes[0].x) / window.canvasObj.easingFactor;
      window.canvasObj.nodes[0].y += (window.canvasObj.mousePos[1] - window.canvasObj.nodes[0].y) / window.canvasObj.easingFactor;
    },
    lengthOfEdge(edge) {
      return Math.sqrt(Math.pow((edge.from.x - edge.to.x), 2) + Math.pow((edge.from.y - edge.to.y), 2));
    },
    render() {
      let that = this;
      // window.canvasObj.ctx.fillStyle = window.canvasObj.backgroundColor;
      // window.canvasObj.ctx.fillRect(0, 0, window.canvasObj.canvasEl.width, window.canvasObj.canvasEl.height);
      window.canvasObj.ctx.clearRect(0, 0, window.canvasObj.canvasEl.width, window.canvasObj.canvasEl.height);
      window.canvasObj.edges.forEach(function (e) {
        var l = that.lengthOfEdge(e);
        var threshold = window.canvasObj.canvasEl.width / 8;

        if (l > threshold) {
          return;
        }

        window.canvasObj.ctx.strokeStyle = window.canvasObj.edgeColor;
        window.canvasObj.ctx.lineWidth = (1.0 - l / threshold) * 2.5;
        window.canvasObj.ctx.globalAlpha = 1.0 - l / threshold;
        window.canvasObj.ctx.beginPath();
        window.canvasObj.ctx.moveTo(e.from.x, e.from.y);
        window.canvasObj.ctx.lineTo(e.to.x, e.to.y);
        window.canvasObj.ctx.stroke();
      });
      window.canvasObj.ctx.globalAlpha = 1;

      window.canvasObj.nodes.forEach(function (e) {
        if (e.drivenByMouse) {
          return;
        }

        window.canvasObj.ctx.fillStyle = window.canvasObj.nodeColor;
        window.canvasObj.ctx.beginPath();
        window.canvasObj.ctx.arc(e.x, e.y, e.radius, 0, 2 * Math.PI);
        window.canvasObj.ctx.fill();
      });
    },
  },
  mounted(){
    window.canvasObj.canvasEl = document.getElementById('canvas');
    window.canvasObj.ctx = document.getElementById('canvas').getContext('2d');
    let that = this;
    window.onresize = function () {
      window.canvasObj.canvasEl.width = document.body.clientWidth;
      window.canvasObj.canvasEl.height = window.canvasObj.canvasEl.clientHeight;

      if (window.canvasObj.nodes.length == 0) {
        that.constructNodes();
      }

      that.render();
    };

    window.onmousemove = function (e) {
      window.canvasObj.mousePos[0] = e.clientX;
      window.canvasObj.mousePos[1] = e.clientY;
    }

    window.onresize(); // trigger the event manually.
    window.requestAnimationFrame(this.step);
  },
  computed:{
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang = "less" scoped>
  .body{
    height: 100%;
    position: absolute;
    z-index: 1000;
    background-image: url("../assets/q.png");
    background-size: cover;
    background-position: center;
    .text{
      position: absolute;
      top: 37%;
      left: 50%;
      transform: translate(-50%,-50%);
      font-size: 0.3rem;
      color: white;
      text-align: center;
      width: 6rem;
    }
   /* img{
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%,-50%);

    }*/
  }
</style>
