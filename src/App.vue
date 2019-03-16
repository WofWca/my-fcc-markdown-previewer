<template>
  <div id="app">
    <textarea
      id="editor"
      v-model="markdown"
      @input="updateMarkup"
    >
      Some default text
    </textarea>
    <section id="preview" v-html="markup">
    </section>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import marked from 'marked';
import defaultMarkdown from './placeholderMarkdown';

marked.setOptions({
  gfm: true,
  silent: true,
});

@Component
export default class App extends Vue {
  private markdown: string = defaultMarkdown;
  private markup: string = '';
  private updateMarkup() {
    this.markup = marked(this.markdown);
  }
  private created() {
    this.updateMarkup();
  }
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
