<script setup lang="ts">
import ButtonCounter from './ButtonCounter.vue'
import BlogPost from '@/BlogPost.vue'
import Home from './Home.vue'
import Post from './Post.vue'
import Archive from './Archive.vue'
import { ref } from 'vue'
import MouseComponent from '@/MouseComponent.vue'

const postFontSize = ref(1)

const currentTab = ref('Home')
const tabs = {
  Home,
  Post,
  Archive,
}
</script>

<template>
  <div :style="{ fontSize: postFontSize + 'em' }">
    <h1>Here is a child component!</h1>
    <ButtonCounter />
    <ButtonCounter />
    <ButtonCounter />
    <BlogPost title="My journey with Vue" />
    <BlogPost title="Blogging with Vue" @enlarge-text="postFontSize += 0.3" />
    <BlogPost title="Why Vue is so fun" @enlarge-text="postFontSize += 0.1" />
    <MouseComponent />

    <div>
      <button
        v-for="(_, tab) in tabs"
        :key="tab"
        @click="currentTab = tab"
      >
        {{tab}}
      </button>
      <component :is="tabs[currentTab]"></component>

    </div>

  </div>

</template>

<style scoped></style>
