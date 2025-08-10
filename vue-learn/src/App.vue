<script setup lang="ts">
  import type { ButtonHTMLAttributes } from 'vue'

  const message = "message is here"
  const additionalMessage = "extra information"

  const buttonProps: ButtonHTMLAttributes = {
    id: 'submitBtn',
    type: 'submit',
    disabled: false
  };

  const isButtonDisabled = true;
</script>


<template>

  <h1>You did it!</h1>
  <p>Hi</p>
  <p>Please enter the message</p>
  <p> {{message}} + {{additionalMessage}}</p>




  <!-- Take JS var dynamicId and set it as the value of the HTML attribute id for this div
       If dynamicId changes in the component, Vue will automatically update the id in the DOM. -->
  <button v-bind="buttonProps">Submit</button>

  <br><br><br>
  <button :disabled="isButtonDisabled">Button</button>
  <br><br><br>


</template>

<style scoped></style>
