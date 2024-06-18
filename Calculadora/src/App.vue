<script lang="ts">
import TitleComponent from "./components/TitleComponent/title-component.vue"
import { Calculator } from "./utils/calculator";

export default {
  name: "App",
  data() {
    let valueInput1 = 1
  },
  components: {
    TitleComponent
  },
  computed: {
    calculator(): Calculator {
      return new Calculator()
    }
  },
  methods:{
    onclick() {
      let result = this.calculator.division();
    }
  }

}
</script>

<template>
  <TitleComponent />
</template>

<style scoped>

</style>
