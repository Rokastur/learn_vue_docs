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
  books: ['Vue 2 - Advanced Guide', 'Vue 3 - Basic Guide', 'Vue 4 - The Mystery'],
})

const anotherAuthor = reactive({
  name: 'For Bro',
  books: [],
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

// compute can be used as a function. The only difference:
// computed properties are cached based on their reactive dependencies
function calculateBooksMessage() {
  return author.books.length > 0 ? 'Yes' : 'No'
}

const isActive = ref(true)
const error = ref<{ type?: string } | null>(null)

const classObject = computed(() => ({
  active: isActive.value && !error.value,
  'text-danger': error.value?.type === 'fatal'
}))

function toggleError() {
  error.value = error.value ? null : { type: 'fatal' }
}

function toggleActive() {
  isActive.value = !isActive.value
}

const name = ref('Vue.js')

function greet(event) {
  alert(`Hello ${name.value}!`)
  if (event) {
    alert(event.target.name)
  }
}
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
  <br /><br /><br />
  <br /><br /><br />
  <button @click="book.year++">book: {{ book }}</button>
  <br /><br /><br />
  <p>Has {{ author.name }} published books?</p>
  <span>{{ hasBooksPublished }}</span>
  <p>Has {{ anotherAuthor.name }} published books?</p>
  <span>{{ hasBooksPublishedAnother }}</span>
  <br /><br /><br />
  <p>{{ calculateBooksMessage() }}</p>
  <br /><br /><br />
  <!--  Presence of active is determined by truthy value of isActive-->
  <div :class="classObject">
    This is a test div.
  </div>

  <button @click="toggleActive">Toggle Active</button>
  <button @click="toggleError">Toggle Error</button>
  <br /><br /><br />
  <button @click="greet">Greet</button>
</template>


<style scoped></style>
<style scoped>
.active {
  background-color: lightgreen;
}

.text-danger {
  color: white;
  background-color: red;
}
</style>
