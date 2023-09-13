

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank">create-vue</a>, the official Vue + Vite
    starter
  </p>
  <p>
    Install
    <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
  <div>{{ cat }}</div>
  <div>{{ person.fullName }}===========</div>
  <div>point{{ point }}</div>
  <div>name2{{ name2 }}</div>
  <div>name3{{ name3 }}</div>
  <button @click="num++">{{ num }}</button>
  <!-- <div>{{ say('hello') }}</div> -->
  <ActionVue :actNum="actNum" @handleChange="actNumAdd" ref="childeRef" />
  <!-- <button @click="actNumAdd()">actNumAdd</button> -->
</template>

<script setup>
import { ref, onMounted, computed, watch, watchEffect, reactive, toRef, toRefs } from 'vue'
import { say } from './action'
import ActionVue from './action.vue'
import usePoint from '../hooks/usePoint'
defineProps({
  msg: String,
})
let person = ref({
  firstName: 'aaa',
  lastName: 'bbb'
})

let human = reactive({
  age: 18,
  name: 'xxx'
})
const name2 = toRef(human, 'name')
const name3 = toRefs(human)



say('hello')
const cat = 'cat'

const num = 0

const childeRef = ref()

const count = ref(0)
console.log('aaaaaaaaaa');
const actNum = ref(0)
function actNumAdd (num) {
  actNum.value = actNum.value + 1
  person.value.fullName = computed(() => {
    return person.value.firstName + '===' + actNum.value + ''
  })
  console.log('actNumAdd', num);

}
watch(person.value, (newValue, oldValue) => {
  console.log('newValue', newValue);
  console.log('oldValue', oldValue);
})

watchEffect(() => {
  let fullName = person.value.fullName
  console.log('person.value', person.value.fullName);
  console.log('watchEffect被调用了');
})
const point = ref(0)
point.value = usePoint(6)
console.log('usePoint(6)', usePoint(6));

onMounted(() => {
  console.log('childeRef.value.childeMeg', childeRef.value.childeMeg)
  childeRef.value.childFn('aaaaaa')
})

</script>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
