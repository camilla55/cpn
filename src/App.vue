<template>
  <div id="app">
    <test-cpn :title="pTitle" :message="pMessage"></test-cpn>
    <test-cpn :title="pTitle1" :message="pMessage1"></test-cpn>
    <cpn-input 
    :number1="num1" 
    :number2="num2"
    @num1Change = "num1Change"
    @num2Change = "num2Change"
    />
  </div>
</template>

<script>
import TestCpn from './components/TestCpn.vue'
import cpnInput from './components/cpnInput.vue'
export default {
  name: 'App',
  components: {
    TestCpn,
    cpnInput
  },
  data(){
    return{
      /*
      多次调用组件，互不影响
      */
      pTitle:"我是标题",
      pMessage:"我是内容，哈哈哈哈哈",
      pTitle1:"我是标题1",
      pMessage1:"我是内容，哈哈哈哈哈1",
      num1:1,
      num2:2,
    }
  },
  methods:{
    num1Change(value){
      //num1是Number类型，value是String类型，需要转换
      this.num1 = parseFloat(value);
    },
    num2Change(value){
      this.num2 =  parseFloat(value)
    }
  }
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
