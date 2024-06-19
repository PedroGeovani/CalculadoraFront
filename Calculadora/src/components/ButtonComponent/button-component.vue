<template>
    <div>    
        <button @click="sendValue">{{ title }}</button>
    </div>
</template>

<script lang="ts">
export default {
    name:'SendValue', // renomear o componente
    emits:['onSendValue'],
    props:{
        title: String,
    },
    methods: {
        sendValue() {
            this.$emit('onSendValue',this.title)
        }
    }
    
}
</script>