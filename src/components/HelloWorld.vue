<script setup lang="ts">
import { ref, onMounted, watch, reactive, computed, nextTick } from 'vue'

const props = defineProps<{ msg: string }>()

const count = ref(0)
const str = ref('')
const input = ref<HTMLInputElement | null>(null)
const author = reactive({
  name: 'sds',
  age: 22,
  book: [
    'book1',
    'book2'
  ]
})
const flag = ref(false)

const age = computed(() => {
  return author.age > 24 ? '太大了' : '还小'
})

onMounted(() => {
  console.log(`hello`);
  console.log(props.msg);
  input.value?.focus()
})

watch(str,async (newValue, oldValue) => {
  console.log(newValue, oldValue);
})

function handlerClick(event: Event) {
  author.age++
  author.book.push("book"+author.age)
  nextTick(() => {
    console.log("dom update done");
    console.log(author);
  })
  console.log("end");
  console.log(author);
  flag.value = !flag.value
  // console.log((event.target as HTMLButtonElement).value);
}
</script>

<template>
  <h1>{{ msg }}</h1>
  <button type="button" @click="count++">count is: {{ count }}</button>
  <input type="text" v-model="str" ref="input">
  <button type="button" @click="handlerClick">点击事件</button>
  <p>{{ author }}</p>
  <p>{{ age }}</p>
  <p v-if="flag">条件渲染</p>
  <p v-else>默认渲染</p>
</template>

<style scoped>
a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}
</style>
