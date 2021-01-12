<template>
  <div id="app">
    <button @click="submit">提交</button><br/>

    <div class="markdownEditorDiv">
      <mavon-editor class="markdownEditor" v-model="value" @imgAdd="addImageCallback" @imgDel="deleteImageCallback" />
    </div>

  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      value: ""
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
</style>
