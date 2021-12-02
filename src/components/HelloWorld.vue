<template>
  <div class="container">
    <canvas
      id="field"
      width="800"
      height="600"
      ref="canva"
    ></canvas>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, onMounted, ref } from "vue";
import Mouse from "./classes/Mouse";
import Ball from "./classes/Ball";

export default defineComponent({
  name: "HelloWorld",
  
  setup() {
    
    var particles = 1
    var balls: Array<Ball> = new Array<Ball>();
    var ctx:CanvasRenderingContext2D|null
    var mouse:Mouse|null
    var cursor:Ball
    onMounted(() => {
      const canvas: HTMLCanvasElement = document.querySelector('canvas') as any;
      ctx = canvas.getContext("2d");
      mouse = new Mouse(canvas);
      
      cursor = new Ball(ctx!, 0, 0, 30, "#22cc1933",undefined,undefined);
      updateData(1,0.5,0.01)
      
      Render();
    });
    const updateData = (pars:number,fr:number, sp:number)=>{
      particles = pars
      balls = new Array<Ball>()
      for (let i = 0; i < particles; i++) {
        let x = Math.random() * 800;
        let y = Math.random() * 600;
        let ball = new Ball(ctx!, x, y, 3, "#30aaff",fr,sp);
        balls.push(ball);
      }
    }
    function Render() {
      window.requestAnimationFrame(Render);
      ctx!.clearRect(0, 0, 800, 600);

      balls.forEach((item) => {
        item.draw();
        item.think(mouse!.x, mouse!.y);
      });
      cursor.setPos(mouse!.x, mouse!.y);
      cursor.draw();
    }
    return { updateData };
  },
});
</script>


<style scoped>
canvas{
    border: 1px solid #333;
    
}
</style>
