<template>
 <div class="background">
  <div> 
    <TitleComponent class="header"/>        
    <li class="display">  {{ textOut }} </li> 
  </div>
      
    <div>
      <button class="button" @click= "valueInput(tag[0])"> {{ tag[0] }} </button>
      <button class="button" @click= "valueInput(tag[1])"> {{ tag[1] }} </button>
      <button class="button" @click= "valueInput(tag[2])"> {{ tag[2] }} </button>
      <button class="button" @click= "valueInput(tag[3])"> {{ tag[3] }} </button>
    </div>
    <div>
      <button class="button" @click= "valueInput(tag[4])"> {{ tag[4] }} </button>
      <button class="button" @click= "valueInput(tag[5])"> {{ tag[5] }} </button>
      <button class="button" @click= "valueInput(tag[6])"> {{ tag[6] }} </button>
      <button class="button" @click= "valueInput(tag[7])"> {{ tag[7] }} </button>
    </div>
    <div>
      <button class="button" @click= "valueInput(tag[8])"> {{ tag[8] }} </button>
      <button class="button" @click= "valueInput(tag[9])"> {{ tag[9] }} </button>
      <button class="button" @click= "valueInput(tag[10])"> {{ tag[10] }} </button>
      <button class="button" @click= "valueInput(tag[11])"> {{ tag[11] }} </button>
    </div>
    
    <div>
      <button class="button" @click= "clear()"> {{ tag[12] }} </button>
      <button class="button" @click= "valueInput(tag[13])"> {{ tag[13] }} </button>
      <button class="button" @click="valueInput(tag[14])"> {{ tag[14] }} </button>       
      <button class="button" @click="valueInput(tag[15])"> {{ tag[15] }} </button>       
    </div>
  </div> 
</template>

<script lang="ts"> 
import TitleComponent from "./components/TitleComponent/title-component.vue"
import ButtonComponent from "./components/ButtonComponent/button-component.vue"
export default {
  name: "App",
  data() {
    return{ 
      tag : ['1','2','3','+','4','5','6','-','7','8','9','x','CE','0','=','/'],      
      signal : "SIGNAL",
      correntInput : "SIGNAL",
      textOut : "",
      value1 : 0,
      value2 : 0,
      result : 0,
      counter : 0,
    }    
  },
  components: {    
    ButtonComponent,
    TitleComponent,   
  },
  methods: {
    displayOut(): string { //saida do display
      switch(this.counter){        
        case 0: return (String(this.value1))
          break
        case 1: return (String(this.value1) + this.signal) 
          break
        case 2: return (String(this.value1) + this.signal + String(this.value2)) 
          break
        case 3: return (String(this.value1) + this.signal + String(this.value2) + " = " + String(this.result))
         break
        default : return  ""
      }
    },

    clear(){  //limpar tudo    
        this.signal = "SIGNAL"        
        this.value1 = 0
        this.value2 = 0
        this.textOut = ""
        this.counter = 0
        this.result = 0      
    },

    typeInput(keyboardInput: string): string{ //verifica o tipo de entrada
      switch(keyboardInput){
        case '+':
        case '-':
        case 'x':
        case '/':
        case 'CE': 
        case '=' : return "SIGNAL" 
          break
        default : return "NUMBER"
      }
    },

    operation(signal: string, value1: number, value2: number):number{ // faz as operações
      switch(signal){
        case '+':return (value1+value2)
          break
        case '-':return (value1-value2)
          break
        case 'x':return (value1*value2)
          break
        case '/':return (value1/value2)
          break
        default: return 0
      }
    },

    valueInput(keyboardInput: string){ //gerencia a entrada de valores e sinais 
      if(keyboardInput == "="){    
        if(this.signal == "SIGNAL"){ this.signal = '+'}    
        this.result = this.operation(this.signal, this.value1, this.value2) 
        this.counter = 3
      }else if(this.counter == 0){
        if(this.typeInput(keyboardInput) == "NUMBER"){
          this.value1 = 10*this.value1 + Number(keyboardInput)
        }else{
          this.signal = keyboardInput
          this.counter = 1
        }
      }else if(this.counter == 1){
        if(this.typeInput(keyboardInput) == "NUMBER"){
          this.value2 = 10*this.value2 + Number(keyboardInput)
          this.counter = 2
        }else{
          this.signal = keyboardInput
        }        
      }else if(this.counter == 2){
        if(this.typeInput(keyboardInput) == "NUMBER"){
          this.value2 = 10*this.value2 + Number(keyboardInput)        
        }
      }
      this.textOut = this.displayOut()     
    }
  }
}
</script>

<style scoped>
  .button{
    background: black;
    font-size: 50px;
    text-align: center;
    color: white;
    width: 100px;
    height: 100px;
    border-radius: 15px;
  }    
  .header{    
    font-size: 50px;
    text-align: center;
    color: white;
    align-content: center;
    width: 396px;
    height: 80px;
    margin-left: 10px;
    border-width: 2px; 
    border-style: solid; 
    border-color: white;
    border-top-right-radius: 15px;
    border-top-left-radius: 15px;
  }
  
  .display{
    font-size: 50px;
    color: white;
    text-align: center;
    align-content: center;
    width: 396px;
    height: 80px;
    margin-left: 10px;
    border-width: 2px; 
    border-style: solid; 
    border-color: white;
    border-bottom-left-radius: 15px;
    border-bottom-right-radius: 15px;
  }  
  .background{  
    background: rgb(0, 0, 0);
    align-content: center;
    align-items: center;
    text-align: center;
    border: 3px;
    border-style: solid; 
    border-color:  white;
    border-bottom-color: white;
    border-radius: 20px;
    width: 420px;
    height: 590px;
  }  
</style>

