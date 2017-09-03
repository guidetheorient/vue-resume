<template>
    <div id="topbar">
        <div class="logo">
            <svg class="icon" aria-hidden="true">
                <use xlink:href="#icon-jianliguanli"></use>
            </svg>
            在线简历编辑器
        </div>
        <div class="actions">
            <el-button class="text-button" type="text" @click="signUpDialogVisible = true" v-if="!currentUser">注册</el-button>
            <span class="vertical-line" v-if="!currentUser">|</span>
            <el-button class="text-button" type="text" @click="loginDialogVisible = true" v-if="!currentUser">登录</el-button>
            <el-button type="success" v-on:click="preview">预览</el-button>
            <el-button @click="saveOrUpdateResume" v-if="currentUser">保存</el-button>
            <el-button @click="logout" v-if="currentUser">登出</el-button>
        </div>
        <el-dialog v-if="!currentUser" size="tiny" class="login" title="注册" :visible.sync="signUpDialogVisible" :modal-append-to-body="false">
            <el-form :model="form">
                <el-form-item label="用户名">
                    <el-input v-model="form.username"></el-input>
                </el-form-item>
                <el-form-item label="密码">
                    <el-input v-model="form.password"></el-input>
                </el-form-item>
            </el-form>
            <div slot="footer" class="dialog-footer">
                <el-button @click="signUpDialogVisible = false">取 消</el-button>
                <el-button type="primary" @click="signUp">注 册</el-button>
            </div>
        </el-dialog>
        <el-dialog v-if="!currentUser" size="tiny" class="login" title="登录" :visible.sync="loginDialogVisible" :modal-append-to-body="false">
            <el-form :model="form">
                <el-form-item label="用户名">
                    <el-input v-model="loginForm.username"></el-input>
                </el-form-item>
                <el-form-item label="密码">
                    <el-input v-model="loginForm.password"></el-input>
                </el-form-item>
            </el-form>
            <div slot="footer" class="dialog-footer">
                <el-button @click="loginDialogVisible = false">取 消</el-button>
                <el-button type="primary" @click="login">登录</el-button>
            </div>
        </el-dialog>
    </div>
</template>
<script>
import AV from '../lib/leancloud'

export default {
    props: ['resume'],
    data() {
        return {
            currentUser: null,
            signUpDialogVisible: false,
            loginDialogVisible: false,
            form: {
                username: '',
                password: '',
            },
            loginForm: {
                username: '',
                password: '',
            },
            formLabelWidth: '120px',
            resumeContent: ''
        }
    },
    created() {
        this.currentUser = this.getCurrentUser()
        this.fetchResumeContent()
    },
    methods: {
        preview() {
            this.$emit('preview')
        },
        fetchResumeContent() {
            if (this.currentUser) {
                var query = new AV.Query('Resumefolder')
                query.find()
                    .then((resume) => {
                        let avResume = resume[0]
                        let id = avResume.id
                        this.resumeContent = JSON.parse(avResume.attributes.content)
                        console.log(this.resumeContent, 33)
                        this.resumeContent.id = id
                        this.$emit('update:resume', this.resumeContent)
                    }, function(error) {
                        console.error(error)
                    })
            }

        },
        signUp() {
            this.signUpDialogVisible = false;
            let user = new AV.User();
            // 设置用户名
            user.setUsername(this.form.username);
            // 设置密码
            user.setPassword(this.form.password);

            user.signUp().then((loginedUser) => {
                // console.log(loginedUser)
                this.currentUser = this.getCurrentUser()
            }, function(error) {
                console.log('注册失败')
            });
        },
        login() {
            AV.User.logIn(this.loginForm.username, this.loginForm.password).then((loginedUser) => {
                this.currentUser = this.getCurrentUser();
                this.loginDialogVisible = false;
                this.fetchResumeContent()
            }, function(error) {
                console.log('登录失败')
            });
        },
        getCurrentUser() {
            let current = AV.User.current()
            if (current) {
                let { id, createdAt, attributes: { username } } = AV.User.current()
                return { id, username, createdAt }
            } else {
                return null
            }
        },
        logout() {
            AV.User.logOut()
            this.currentUser = null
            window.location.reload()
        },
        saveOrUpdateResume: function() {
            if (this.resume.id) {
                this.updateResumeContent()
            } else {
                this.saveResumeContent()
            }
        },
        saveResumeContent() {
            let session = JSON.stringify(this.resume)
            var Resumefolder = AV.Object.extend('Resumefolder')
            var resumefolder = new Resumefolder()

            //设置当前content的只可以被当前登录的用户读写
            var acl = new AV.ACL()
            acl.setReadAccess(AV.User.current(), true)
            acl.setWriteAccess(AV.User.current(), true)

            resumefolder.set('content', session)

            resumefolder.setACL(acl)

            resumefolder.save().then((resume) => {
                this.resume.id = resume.id
                console.log('保存成功')
            }, function(error) {
                alert('保存失败')
            })
        },
        updateResumeContent: function() {
            let session = JSON.stringify(this.resume)
            let avResume = AV.Object.createWithoutData('Resumefolder', this.resume.id)
            avResume.set('content', session)
            avResume.save().then(() => {
                console.log('更新成功')
            })
        },
    }
}
</script>

<style>
#topbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 16px;
    font-size: 24px;
    font-weight: 500;
    color: #fff;
    background-color: #1D8CE0;
}
#topbar > .logo{
    font-family: 'KaiTi';
}
#topbar > .logo .icon{
    fill:#fff;
    font-size: 40px;
    vertical-align: -0.28em;    
}
#topbar .text-button{
    color:#fff;
}
#topbar .text-button+.vertical-line{
    font-size: 20px;
    word-spacing: 0.4em;
}

</style>