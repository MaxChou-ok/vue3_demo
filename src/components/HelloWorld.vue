<template>
  <h1>{{ msg }}</h1>

  <p>
    <a href="https://vitejs.dev/guide/features.html" target="_blank">
      Vite Documentation
    </a>
    |
    <a href="https://v3.vuejs.org/" target="_blank">Vue 3 Documentation</a>
  </p>

  <button @click="counter++">count is: {{ counter }}</button>
  <p>
    Edit
    <code>components/HelloWorld.vue</code> to test hot module replacement.
  </p>
  <p>{{counter}}</p>
  <p>{{doubleCounter}}</p>
  <p ref="desc"></p>

  <ModelButton></ModelButton>
  
  <Emits @my-click="onClick"></Emits>
</template>

<script>
import { computed, onMounted, onUnmounted, reactive, ref, toRefs, watch } from 'vue'
import ModelButton from './ModelButton.vue'
import Emits from './Emits.vue'

export default {
 name:'helloword',
 props:{
   msg:String
 },
 components:{
   ModelButton,
   Emits
 },
 methods:{
   onClick() {
     console.log('click');
   }
 },
 setup(){

  const {counter,doubleCounter} = useCounter()
  const msg2 = ref('message');
  const desc = ref(null)

  watch(counter,(val,oldVal)=>{
   const p = desc.value
   p.textContent = `counter change from ${oldVal} to ${val}`
  })

   return { counter, doubleCounter, msg2, desc}
 }
}

function useCounter() {
   const data = reactive({
   counter:1,
   doubleCounter:computed(()=> data.counter *2)
   })
     let timer

  onMounted(()=>{
  timer =  setInterval(()=>{
     data.counter++
   },1000)
  })

  onUnmounted(()=>{
    clearInterval(timer)
  })

  return toRefs(data)
}






// const state = reactive({
//   count: 1,
//   doubleCounter:computed(()=> state.count *2)
// })
  
//   let timer
//   onMounted(()=>{
//   timer =  setInterval(()=>{
//      state.count++
//    },1000)
//   })

//   onUnmounted(()=>{
//     clearInterval(timer)
//   })

//  const state = useCounter()
//  const msg2 = ref('some message')
//  const desc = ref(null)
 
//  watch(()=> state.count,(val,oldVal)=>{
//    const p =  desc.value
//    p.textContent = `counter change from ${oldVal} to ${val}`
//  })


//  function useCounter(){
//    const state = reactive({
//     count: 1,
//     doubleCounter:computed(()=> state.count *2),
// })
  
//   let timer
//   onMounted(()=>{
//   timer =  setInterval(()=>{
//      state.count++
//    },1000)
//   })

//   onUnmounted(()=>{
//     clearInterval(timer)
//   });

//   return state
//  }



</script>
 
<style scoped>
a {
  color: #42b983;
}
</style>
