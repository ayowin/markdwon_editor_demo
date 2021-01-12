<template>
  <div id="app">
    <button @click="submit">提交</button><br/>

    <div class="markdownEditorDiv">
      <mavon-editor class="markdownEditor" v-model="value" @imgAdd="addImageCallback" @imgDel="deleteImageCallback" />
    </div>


    <h1>markdown与html混合预览技术（基于marked）：</h1>
    <div class="markedDiv">
      <div v-html="computedMarkedObject"></div>
    </div>
  </div>
</template>

<script>
import marked from 'marked'

/* marked初始化：语法高亮等效果 */
marked.setOptions({
  renderer: new marked.Renderer(),
  highlight: function(code, language) {
    const hljs = require('highlight.js');
    const validLanguage = hljs.getLanguage(language) ? language : 'plaintext';
    return hljs.highlight(validLanguage, code).value;
  },
  pedantic: false,
  gfm: true,
  breaks: false,
  sanitize: false,
  smartLists: true,
  smartypants: false,
  xhtml: false
});

export default {
  name: 'App',
  data() {
    return {
      value: ""
    }
  },
  computed: {
    computedMarkedObject : function () {
      return marked ( this.value, { sanitize: true });
    }
  },
  methods: {
    submit: function(){
      console.log("value: " + this.value);
    },
    addImageCallback: function(filename,file){
      console.log("filename:" + filename);
      console.log("file:" + file);
    },
    deleteImageCallback: function(filename){
      console.log("filename:" + filename);
    }
  }
}
</script>

<style>
#app {
  text-align: center;
}
.markdownEditorDiv{
  width: 90%;
  height: 800px;
  display: inline-block;
}

.markdownEditor{
  width: 100%;
  height: 100%;
}

.markedDiv{
  background-color: lightblue;
  padding: 10px 5% 10px 5%;
  text-align: left;
}
</style>
