<script lang="ts">
import TitleComponent from "./components/TitleComponent/title-component.vue"
import ButtonComponent from "./components/ButtonComponent/button-component.vue";
import { Calculator } from "./utils/calculator";

export default {
  name: "App",
  data() {
   let value1 : ""
   let value2 : ""
    
  },
  components: {
    ButtonComponent,
    TitleComponent,

    let simbolCalculator = new Vue(
      e1 : 'testo',
      data : {
         itens :  [{tag: "1"},
                  {tag: "2"},
                  {tag: "3"},
                  {tag: "4"},
                  {tag: "4"},
                  {tag: "5"},
                  {tag: "6"}]                
              }),

  computed: {
    calculator(): Calculator {
      return new Calculator()
    }
  },
  methods:{
    onclick() {
      // let result = this.calculator.division();
    }
  }


</script>

<template>
  <div>
    <TitleComponent />
  <div>

    <ul id = "vetor">
      <p v-for="(item, index) in ">
         {{ item [index] }}
      </p>       
    </ul>     
  </div>
  </div>
 
</template>

<style scoped>

</style>
