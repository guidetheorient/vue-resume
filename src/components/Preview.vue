<template>
    <div id="preview">
        <div class="header"></div>
        <div class="main">
            <section class="profile">
                <div class="info-title">
                    <svg class="icon" aria-hidden="true">
                        <use xlink:href="#icon-shenfen"></use>
                    </svg>
                    <span class="title">个人信息</span>
                </div>
                <ul class="info">
                    <li>姓&nbsp;&nbsp;&nbsp;&nbsp;名:
                        <span>{{resume.profile.name || '姓名'}}</span>
                    </li>
                    <li>城&nbsp;&nbsp;&nbsp;&nbsp;市:
                        <span>{{resume.profile.city || '城市'}}</span>
                    </li>
                    <li><span>出生年月:</span>
                        <span>{{resume.profile.birth || '出生年月'}}</span>
                    </li>
                    <li>手&nbsp;&nbsp;&nbsp;&nbsp;机:
                        <span>{{resume.contacts.phone || '手机'}}</span>
                    </li>
                    <li>邮&nbsp;&nbsp;&nbsp;&nbsp;箱:
                        <span>{{resume.contacts.email || '邮箱'}}</span>
                    </li>
                    <li>Q&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Q:
                        <span>{{resume.contacts.phone || 'QQ'}}</span>
                    </li>
                    <li class="letter-space">Github:
                        <span>{{resume.contacts.github || 'github'}}</span>
                    </li>
                </ul>
            </section>
            <section class="work-history" v-if="filter(resume.workHistory).length > 0">
                <div class="info-title">
                    <svg class="icon" aria-hidden="true">
                        <use xlink:href="#icon-gongzuojingli"></use>
                    </svg>
                    <span class="title">工作经历</span>
                </div>
                <ul v-for="(item,index) in resume.workHistory" :key="index" class="one-work-history">
                    <li class="work-title">
                        <p class="duration">{{item.duration}}</p>
                        <p class="company">{{item.company}}</p>
                    </li>
                    <li class="work-content">{{item.content}}</li>
                </ul>
            </section>
            <section class="projects" v-if="filter(resume.projects).length > 0">
                <div class="info-title">
                    <svg class="icon" aria-hidden="true">
                        <use xlink:href="#icon-xiangmu2"></use>
                    </svg>
                    <span class="title">项目经历</span>
                </div>
                <ul v-for="(item,index) in resume.projects" :key="index" class="one-work-history">
                    <li class="work-title">
                        <p class="company">{{item.name}}</p>
                    </li>
                    <li class="work-content">{{item.content}}</li>
                </ul>
            </section>
            <section class="study-history" v-if="filter(resume.studyHistory).length > 0">
                <div class="info-title">
                    <svg class="icon" aria-hidden="true">
                        <use xlink:href="#icon-yinhang-copy"></use>
                    </svg>
                    <span class="title">学习经历</span>
                </div>
                <ul v-for="(item,index) in resume.studyHistory" :key="index" class="one-work-history">
                    <li class="work-title">
                        <p>{{item.duration}}</p>
                        <p>{{item.school}}</p>
                        <p>{{item.degree}}</p>
                    </li>
                    <li class="work-content"></li>
                </ul>
            </section>
            <section class="awards" v-if="filter(resume.awards).length > 0">
                <div class="info-title">
                    <svg class="icon" aria-hidden="true">
                        <use xlink:href="#icon-jiangbei"></use>
                    </svg>
                    <span class="title">获奖情况</span>
                </div>
                <ul v-for="(item,index) in resume.awards" :key="index" class="one-work-history">
                    <li class="work-title">
                        <p>{{item.name}}</p>
                    </li>
                    <li class="work-content">{{item.content}}</li>
                </ul>
            </section>
            <section v-if="filter(resume.workHistory).length > 0">
            </section>
        </div>

    </div>
</template>
<script>
export default {
    props: ['resume'],
    methods: {
        filter(array) {
            return array.filter(item => !this.isEmpty(item))
        },
        isEmpty(object) {
            let empty = true
            for (let key in object) {
                if (object[key]) {
                    empty = false
                    break
                }
            }
            return empty
        }
    }
}
</script>

<style>
/* #preview{
        min-height:100px;
    } */

#preview {
    font-family: "microsoft yahei", "sans-serif";
    color:#324057;
}

#preview .header {
    height: 28px;
    margin: 32px 0;
    background-color: #20A0FF
}

#preview .main {
    margin: 0 48px;
}

.header::before {
    content: '';
    display: block;
    height: 28px;
    width: 8px;
    background-color: #fff;
    position: relative;
    left: 32px;
}

section .icon {
    width: 35px;
    height: 35px;
    padding: 5px;
    background-color: #20A0FF;
    fill: #fff;
    border-radius: 50%;
    vertical-align: middle;
}

.info-title {
    vertical-align: middle;
}

.info-title .title {
    color: #20A0FF;
    font-size: 17px;
    font-weight: 600;
    vertical-align: middle;
}

.profile ul.info {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    margin: 15px 10px;
    font-family: "YouYuan", "microsoft yahei", "sans-serif";
}

.profile .info li {
    display: inline-block;
    margin-bottom: 12px;
    font-size: 16px;
    width: 50%;
}

li.letter-space {
    /* letter-spacing: 2.7px; */
}
.one-work-history{
    margin: 15px 10px 20px;
}
.one-work-history .work-title{
    font-weight: 600;
    margin-bottom: 15px; 
}
.work-title > p{
    display: inline-block;
    width: 210px;
}
.one-work-history .work-content{
    font-family: "YouYuan", "microsoft yahei", "sans-serif";    
}
</style>