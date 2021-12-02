<template>
  <h1>Jelly effect</h1>
  <HelloWorld :particles="particles" ref="jelly"/>
  <div class="panel">
   <div class="control">
     <div>Particles</div>
     <div style="width:600px">
       <el-slider v-model="particles_value" :min="1" :max="4000"/>
      </div>
    </div>
   <div class="control"><div>Glide</div><div style="width:600px"><el-slider v-model="friction" :min="1" :max="1000"/></div></div>
   <div class="control"><div>Spring</div><div style="width:600px"><el-slider v-model="spring" :min="1" :max="1000"/></div></div> 
   
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, Ref, ref, watch } from 'vue';
import HelloWorld from './components/HelloWorld.vue';


export default defineComponent({
  name: 'App',
  components: {
    HelloWorld
  },
  setup(){
    const jelly:Ref<any> = ref(null)
    const particles_value = ref(1)
    const friction = ref(1)
    const spring = ref(1)
    watch([particles_value,friction,spring],(newVal,oldVal)=>{
      jelly.value.updateData(newVal[0],newVal[1]/1000,newVal[2]/1000)
    })
    return {jelly,particles_value,friction,spring}
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #212d3a;
  margin-top: 60px;
}
.panel{
  width: 800px;
  margin: auto;
}
.control{
  display: flex;
  align-items: center;
  justify-content: space-between;

}
</style>
