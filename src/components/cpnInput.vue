<template>
    <div>
    <p>props:<b>{{ number1 }}</b></p>
    <p>data:<b>{{ dnumber1 }}</b></p>
    <!-- <input type="text" v-model="dnumber1"> -->
     <input type="text" :value="dnumber1" @input="dnumber1Input">
    <p>props:<b>{{ number2 }}</b></p>
    <p>data:<b>{{ dnumber2 }}</b></p>
    <!-- <input type="text" v-model="dnumber2"> -->
    <input type="text" :value="dnumber2" @input="dnumber2Input">
    <!-- <button @click="increaseFn">+</button>
    <button @click="reduceFn">-</button> -->
    </div>
</template>

<script>
/*
需求：
1.子组件中的input值改变，同时父组件中的值也相应修改
2.number2的值是number1的100倍，number1是number2的1/100

注意：不要在子组件中修改props中的值，否则会报错
通过$emit事件 把value传出去，用于修改父组件中的值

*/
export default{
  props:{
    number1:Number,
    number2:Number
  },
  data(){
    return{
      //根据props中数据初始化data中的数据，用于v-modle中的数据绑定
      dnumber1 : this.number1,
      dnumber2 : this.number2
    }
  },
  methods:{
    // increaseFn(){
    //     this.num++

    // },
    // reduceFn(){
    //   this.num--;
    // }
    dnumber1Input(event){
      //1.将input中的值赋值到dnumber中
      this.dnumber1 = event.target.value;
      //2.为了让父组件可以修改值，发出一个事件，通过$emit事件将value值传递出去，父组件中传方法@num1Change
      this.$emit('num1Change' ,this.dnumber1);
      //3.同时修改dnumber2的值
      this.dnumber2 = this.dnumber1*100;
      //4.dnumber1发生改变时，相应的dnumber2发生改变的值也要传出去
      this.$emit('num2Change' ,this.dnumber2); 
    },
    dnumber2Input(event){
      this.dnumber2 = event.target.value;
      this.$emit('num2Change' ,this.dnumber2);
      //3.同时修改dnumber1的值
      this.dnumber1 = this.dnumber2/100;
      //4.dnumber2发生改变时，相应的dnumber1发生改变的值也要传出去
      this.$emit('num1Change' ,this.dnumber1); 
    }
  }

}
</script>