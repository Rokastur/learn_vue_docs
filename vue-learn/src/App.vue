<script setup lang="ts">
import { type ButtonHTMLAttributes, computed, reactive, ref } from 'vue'

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

const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})

const anotherAuthor = reactive({
  name: 'For Bro',
  books: [
  ]
})

// too much logic in template can make it bloated and hard to maintain. Complex logic can be included
// which includes reactive data use computed property.
const hasBooksPublished = computed(() => {
  return author.books.length > 0 ? 'Yes' : 'No'
})

const hasBooksPublishedAnother = computed(() => {
  return anotherAuthor.books.length > 0 ? 'Yes' : 'No'
})

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
  <br /><br /><br />
  <p>Has {{author.name }} published books?</p>
  <span>{{hasBooksPublished}}</span>
  <p>Has {{anotherAuthor.name }} published books?</p>
  <span>{{hasBooksPublishedAnother}}</span>
</template>

<style scoped></style>
