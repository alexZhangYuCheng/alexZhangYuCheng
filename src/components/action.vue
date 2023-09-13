

<template>
    <h1>action</h1>
    <div>{{ actNum }}</div>
    <button @click="actChange(1)">actChange</button>
</template>
  
<script setup>
import { onBeforeMount, onMounted, onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted } from 'vue'
console.log('start========');
onBeforeMount(() => {
    console.log('onBeforeMount');
})
onMounted(() => {
    console.log('onMounted');
})
onBeforeUpdate(() => {
    console.log('onBeforeUpdate');
})
onUpdated(() => {
    console.log('onUpdated');
})
onBeforeUnmount(() => {
    console.log('onBeforeUnmount');
})
onUnmounted(() => {
    console.log('onUnmounted');
})
const props = defineProps({
    actNum: Number
})
console.log('props.actNum', props.actNum);
const emits = defineEmits(['handleChange'])
function actChange (num) {
    emits('handleChange', num)
}
function childFn (val) {
    console.log('子组件方法:', val);
}
const childeMeg = '子组件内容'
defineExpose({
    childFn,
    childeMeg
})
</script>
  
<style scoped>
.read-the-docs {
    color: #888;
}
</style>
  