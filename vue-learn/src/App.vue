<script setup lang="ts">
import { type ButtonHTMLAttributes, reactive, ref } from 'vue'

const message = 'message is here'
const additionalMessage = 'extra information'

const buttonProps: ButtonHTMLAttributes = {
  id: 'submitBtn',
  type: 'submit',
  disabled: false,
}

const isButtonDisabled = false

//   reactivity:
//recommended way is to use the ref() function.
//ref wraps the argument into an object and provides .value property.
const count = ref(0)
count.value++
const countFunction = ref(0)

function increment() {
  countFunction.value++
}

interface Book {
  title: string
  year?: number
}

const book: Book = reactive({ title: 'learn vue', year: 2000 })
</script>

<template>
  <h1>You did it!</h1>
  <p>Hi</p>
  <p>Please enter the message</p>
  <p>{{ message }} + {{ additionalMessage }}</p>

  <!-- Take JS var dynamicId and set it as the value of the HTML attribute id for this div
       If dynamicId changes in the component, Vue will automatically update the id in the DOM. -->
  <button v-bind="buttonProps" @click="count++">Submit</button>

  <br /><br /><br />
  <button :disabled="isButtonDisabled" @click="count--">Button</button>
  <br /><br /><br />
  <p>Current count value: {{ count }}</p>
  <br /><br /><br />
  <button @click="increment">Function button {{ countFunction }}</button>
  <br /><br /><br /> <br /><br /><br />
  <button @click="book.year++">book: {{ book }}</button>
</template>

<style scoped></style>
