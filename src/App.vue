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
  breaks: true,
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
  display: flex;
  height: 100vh;
  > #editor, #preview {
    overflow-y: scroll;
    text-align: initial;
  }
  > #editor {
    resize: horizontal;
    width: 50%;
    flex-shrink: 0;
  }
  > #preview {
    flex-basis: 100%;
    padding: 10px;
    h1, h2 {
      border-bottom: 1px solid #eee;
    }
    pre, :not(pre) > code {
      background-color: #eee;
      border-radius: 5px;
      padding: 3px 5px;
    }
    blockquote {
      margin-left: 0px;
      padding-left: 40px;
      border-left: 5px solid #ddd;
    }
    table {
      border-spacing: 0;
      border-collapse: collapse;
      tr {
        td, th {
          border: 1px solid #ddd;
          padding: 5px 10px;
        }
        th {
          font-weight: bold;
        }
        &:nth-child(2) {
          background-color: #eee;
        }
      }
    }
  }
}
</style>
