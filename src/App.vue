<template>
  <div id="app" v-bind:class="{previewMode:previewMode}">
    <Topbar class="topbar" v-on:preview="enterPreview"/>
    <main>
      <Editor  class="editor" v-bind:resume="resume"/>
      <Preview class="preview" v-bind:resume="resume"/>
    </main>
    <el-button id="exit-preview" v-on:click="exitPreview">退出预览</el-button>
  </div>
</template>

<script>
import Topbar from './components/Topbar'
import Editor from './components/Editor'
import Preview from './components/Preview'

export default {
  components: {
    Topbar, Editor, Preview
  },
  methods:{
    enterPreview(){
      this.previewMode = true
    },
    exitPreview(){
      this.previewMode = false
    }
  },
  data() {
    return {
      previewMode:false,
      resume: {
        profile: {
          name: '',
          city: '',
          birth: ''
        },
        workHistory: [
          { company: '', content: '' }
        ],
        studyHistory: [
          { school: '', degree: '', duration: '' }
        ],
        projects: [
          { name: '', content: '' }
        ],
        awards: [
          { name: '' }
        ],
        contacts: {
          phone: '', qq: '', wechat: '', email: ''
        }
      }
    }
  }
}
</script>

<style>
html,
body,
#app {
  height: 100%;
  overflow: hidden;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
}

.topbar {
  position: relative;
  z-index: 1;
  box-shadow: 0 0 3px hsla(0, 0, 0, 0.5);
}

#app main {
  display: flex;
  flex: 1;
  background: #eee;
}

.editor {
  width: 40em;
  margin: 16px 8px 16px 16px;
  background: #fff;
}

.preview {
  flex: 1;
  margin: 16px 16px 16px 8px;
  background: #fff;
}

.icon {
  width: 1em;
  height: 1em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
}
.previewMode #topbar{
  display: none;
}
.previewMode #editor{
  display: none;
}
.previewMode #preview{
  max-width: 800px;
  margin: 10px auto;
}
#exit-preview{
  display: none;
}
.previewMode #exit-preview{
  display: block;
  position: fixed;
  right: 20px;
  bottom: 20px;
}
</style>
