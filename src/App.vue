<template>
  <div id="app" v-bind:class="{previewMode:previewMode}">
    <Topbar class="topbar" v-on:preview="enterPreview" :resume.sync="resume"/>
    <main>
      <Editor class="editor" v-bind:resume="resume" :resume.sync="resume"/>
      <Preview class="preview" v-bind:resume="resume"/>
    </main>
    <el-button type="success" id="exit-preview" v-on:click="exitPreview">退出预览</el-button>
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
      },
      getTime(time){
        let year = time.getFullYear()
        let month = time.getMonth()
        let day = time.getDay()
        return 1
        return year+'-'+month
      }
    },
    data() {
      return {
        previewMode:false,
        resume: {
          profile: {
            name: '',
            city: '',
            birth: '',
          },
          workHistory: [
            { duration:'',company: '', content: '' }
          ],
          studyHistory: [
            { school: '', degree: '', duration: '' }
          ],
          projects: [
            { name: '', content: '' }
          ],
          awards: [
            { name: '', content: '' }
          ],
          contacts: {
            phone: '', email: '', qq: '', github: ''
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
    z-index: 2;
    box-shadow: 0 0 3px hsla(0, 0, 0, 0.5);
  }

  #app main {
    display: flex;
    flex: 1;
    background: #eee;
  }

  .editor {
    width: 35em;
    margin: 0px 0px 0px 0px;
    background: #fff;
  }

  .preview {
    flex: 1;
    margin: 0px 0px 0px 0px;
    background: #fcfaf2;
    border-left: 1px solid #d9d9d9;
    overflow: auto;
  }

  .icon {
    width: 1em;
    height: 1em;
    vertical-align: -0.15em;
    fill: currentColor;
    overflow: hidden;
  }
  #app.previewMode{
    display: flex;
    overflow: auto;
  }
  .previewMode #topbar{
    display: none;
  }
  .previewMode #editor{
    display: none;
  }
  .previewMode #preview{
    max-width: 800px;
    min-width: 800px;
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
  /* .form > div:first-child >.el-icon-close{
    display: none;
  } */
</style>