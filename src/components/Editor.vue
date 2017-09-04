<template>
  <div id="editor">
    <nav class="sidebar">
      <ol>
        <li v-for="i in tabCount" v-bind:class="{ active:currentTab === i }" v-on:click="currentTab = i" :key="i">
          <svg class="icon" v-bind:class="'icon-'+icons[i]">
            <use v-bind:xlink:href="'#icon-'+icons[i]"></use>
          </svg>
          <p class="tip">{{infoType[i]}}</p>
        </li>
      </ol>
    </nav>
    <ol class="panels">
      <li v-bind:class="{active:currentTab === 0}">
        <ProfileEditor v-bind:profile="resume.profile"/>
        <!-- <ProfileEditor v-bind:profile="resume.profile" @changeBirth="change"/> -->
        {{test}}
      </li>
      <li v-bind:class="{active:currentTab === 1}">
        <WorkEditor v-bind:items="resume.workHistory" v-bind:labels="{duration:'时间',company:'公司',content:'工作内容'}" title="工作经历" />
      </li>
      <li v-bind:class="{active:currentTab === 2}">
        <ProjectHistoryEditor v-bind:items="resume.projects" v-bind:labels="{name:'项目名称',content:'项目内容'}" title="项目经历" />        
      </li>
      <li v-bind:class="{active:currentTab === 3}">
        <itemHistoryEditor v-bind:items="resume.studyHistory" v-bind:labels="{school:'学校',degree:'学历',duration:'时间'}" title="学习经历" />
      </li>
      <li v-bind:class="{active:currentTab === 4}">
        <itemHistoryEditor v-bind:items="resume.awards" v-bind:labels="{name:'奖项',content:'描述'}" title="获奖情况" />
      </li>
      <li v-bind:class="{active:currentTab === 5}">
        <ContactsEditor v-bind:contacts="resume.contacts" />
      </li>
    </ol>
  </div>
</template>

<script>
  import ProfileEditor from "./ProfileEditor"
  import itemHistoryEditor from "./itemHistoryEditor"
  import WorkEditor from "./WorkEditor.vue"
  import ProjectHistoryEditor from './ProjectHistoryEditor.vue'
  import ContactsEditor from "./Contacts"
  export default {
    components: {
      ProfileEditor,
      itemHistoryEditor,
      ContactsEditor,
      WorkEditor,
      ProjectHistoryEditor
    },
    props: ['resume'],
    data() {
      return {
        test:'',
        currentTab: 0,
        tabCount: this.initTabcount(),
        icons: ['shenfen',  'gongzuojingli', 'xiangmu2', 'yinhang-copy','jiangbei', 'lianxifangshi'],
        infoType:['个人信息','工作经历','项目经历','学习经历','获奖情况','联系方式']
      }
    },
    methods: {
      initTabcount: function() {
        var count = [];
        for (var i = 0; i < 6; i++) {
          count[i] = i
        }
        // console.log(count)
        return count
      },
      // change(msg){
      //   this.test = msg
      // }
    }
    // created(){
    //     setTimeout(() => {
    //         console.log(this.profile)
    //     },)
    // }
  }
</script>

<style>
#editor {
  min-height: 100px;
  display: flex;
}

#editor>.sidebar {
  background: #1F2D3D;
  width: 80px;
}

.sidebar>ol>li {
  height: 72px;
  /* padding: 16px 0; */
  text-align: center;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items:center;
  flex: 1;
}
.sidebar>ol>li:first-child{
  margin-top: 16px;
}
.sidebar>ol>li>.icon {
  width: 24px;
  height: 24px;
  fill: #fff;
}
.sidebar .tip{
  margin-top: 5px;
  font-size: 12px;
  transition: .5s;
  display: none;
}
.sidebar:hover .tip{
  display: block;
  color:#8492A6
}
.sidebar>ol>li.active {
  background: #fff;
}

.sidebar>ol>li.active>.icon {
  fill: #1F2D3D;
}

.panels {
  overflow: auto;
  flex: 1;
}

.panels>li {
  display: none;
  padding: 32px;
}

.panels>li.active {
  display: block;
}

.panels>li>el-form>el-input {
  width: 100%;
}
.profile,.contacts{
  margin:0 10px;
}

.one-work-history {
  position: relative;
}

.one-work-history>.el-icon-close {
  position: absolute;
  right: 0;
  top: 0;
  font-size: 12px;
  line-height: 20px;
  z-index: 1;
  cursor: pointer;
}

.one-work-history>.el-icon-close::before{
  
  z-index: 1;
}

#editor .icon-shenfen {
  width: 28px;
  height: 28px;
}

div>h3:first-child{
  margin-bottom: 20px;
  font-weight: 600;
}


/* #editor .icon-xiangmu---{
  width: 28px;
  height: 28px;
} */
</style>