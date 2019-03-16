<template>
  <div id="app">
    <textarea
      id="editor"
      v-model="markdown"
    >
      Some default text
    </textarea>
    <section id="preview">
      {{ markup }}
    </section>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import defaultMarkdown from './placeholderMarkdown';

@Component
export default class App extends Vue {
  private markdown: string = defaultMarkdown;
  private markup!: string;
}
</script>

<style lang="scss">
body {
  margin: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
