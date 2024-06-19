<template>
  <div>
    <TitleComponent />
    <h3> saida do display: {{ textOut }} </h3>

    <ul v-for="(tag, index) in tags" :key="tag" @click="calc((tags[index]))">     
      <ButtonComponent :title="tag"/>
      <p v-if="((index+1) === 0)"> </p>  
    </ul>

   
  </div> 
</template>

<style scoped>

</style>


<script lang="ts"> 
import TitleComponent from "./components/TitleComponent/title-component.vue"
import ButtonComponent from "./components/ButtonComponent/button-component.vue"
export default {
  name: "App",
  data() {
    return {
      tags : ['1','2','3','+','4','5','6','-','7','8','9','0','=','Clear'],
      controlOperation : 'b',
      signal : 'a',
      textOut : "",
      textInput : "",
      value1 : 0,
      value2 : 0,
    }
    
  },

  components: {    
    ButtonComponent,
    TitleComponent,
    computed: {
      calculator(): Calculator {
        return new Calculator()
      }
    }
  },
  methods: {
      calc(enter : string ){
          if(this.controlOperation == 'b' || enter == "Clear"){
            this.textInput = ""
            this.value1 = 0
            this.value2 = 0
            this.textOut = ""
            this.controlOperation = 'a'
          }

          if(this.controlOperation == 'a' && enter != "Clear"){              
            
            this.textOut += enter 
            if(enter != "+" && enter != "-" && enter != "x" && enter != "/" && enter != "="){
                this.textInput += enter  
            }

            if(enter == '+' || enter == '-' || enter == 'x' || enter == '/' ){         
                this.signal = enter              
                this.value1 = Number(this.textInput)                                    
              this.controlOperation = 'a' 
              this.textInput = ""
            }else if(enter == '='){
              this.value2 = Number(this.textInput)
              this.textOut += this.algebricOperation(this.signal,this.value1,this.value2) 
              this.controlOperation = 'b'
            }            
          }
        },
  algebricOperation(signal: string, value1: number, value2: number ): string{
    switch(signal){
        case '+':
            return String(value1+value2)
        case '-':
            return String(value1-value2) 
        case 'x':
            return String(value1*value2)
        case '/':
            return String(value1/value2)
        default: 
            return ""
    }
  }
}
}
</script>