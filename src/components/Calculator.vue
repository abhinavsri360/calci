<template>
  <div class="calculator">
    <button class="display">{{current || '0'}}</button>
    <button class="btn" @click="clear">C</button>
    <button class="btn" @click="sign">+/-</button>
    <button class="btn" @click="percent">%</button>
    <button class="btn operator" @click="divide">/</button>
    <button class="btn" @click="append(7)">7</button>
    <button class="btn" @click="append(8)">8</button>
    <button class="btn" @click="append(9)">9</button>
    <button class="btn operator" @click="times">x</button>
    <button class="btn" @click="append(4)">4</button>
    <button class="btn" @click="append(5)">5</button>
    <button class="btn" @click="append(6)">6</button>
    <button class="btn operator" @click="minus">-</button>
    <button class="btn" @click="append(1)">1</button>
    <button class="btn" @click="append(2)">2</button>
    <button class="btn" @click="append(3)">3</button>
    <button class="btn operator" @click="add">+</button>
    <button class="btn zero" @click="append(0)">0</button>
    <button class="btn" @click="dot">.</button>
    <button class="btn operator" @click="equal">=</button>
  </div>
</template>

<script>
export default {
  data(){
    return{
      previous: null,
      current:'',
      operator: null,
      operatorClicked: false
    }
  },
  methods:{
    clear(){
      this.current = '';
    },
    sign(){
      this.current =this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`
    },
    percent(){
      this.current = `${parseFloat(this.current)/100}`
    },
    append(number){
      if(this.operatorClicked){
        this.current = ''
        this.operatorClicked = false
      }
      this.current = `${this.current}${number}`
    },
    dot(){
      if(this.current.indexOf('.')===-1)
        this.append('.')
    },
    divide(){
      this.operator = (a,b) => a/b
      this.setPrevious()
    },
    times(){
      this.operator = (a,b) => a*b
      this.setPrevious()
    },
    minus(){
      this.operator = (a,b) => a-b
      this.setPrevious()
    },
    add(){
      this.operator = (a,b) => a+b
      this.setPrevious()
    },
    setPrevious(){
      this.previous = this.current
      this.operatorClicked = true
      this.current = ''
    },
    equal(){
      this.current = `${this.operator(parseFloat(this.current),parseFloat(this.previous))}`
      this.previous = null
    }
  }
}
</script>

<style scoped>
.calculator{
  margin: 0 auto;
  width: 300px;
  height: 500px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  border: 1px solid #333;
}
.display{
  grid-column: 1/5;
  background-color: ghostwhite;
}
.zero{
  grid-column: 1/3;
}
.btn{
  background-color: #eee;
  border: 1px solid #999;
}
.operator{
  background-color: orange;
  color: whitesmoke;
}
button{
  opacity: 0.6;
  border-radius: 5%;
  font-size: 25px;
}
button:hover{
  padding-right: 25px;
  opacity: 1;
}
</style>
