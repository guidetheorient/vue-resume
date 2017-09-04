<template>
  <div>
    <h3>个人信息</h3>
    <el-form class="profile">
      <el-form-item label="姓名">
        <el-input v-model="profile.name"></el-input>
      </el-form-item>
      <el-form-item label="城市">
        <el-input v-model="profile.city"></el-input>
      </el-form-item>
      <el-form-item label="出生年月">
        <!-- <el-col>
          <el-date-picker type="date" placeholder="选择日期" @change="updateBirth" v-model="birth" style="width: 100%;"></el-date-picker>
        </el-col> -->
        <el-input v-model="profile.birth"></el-input>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  props: ["profile"],
  // data(){
  //   return{
  //     birth:''
  //   }
  // },
  // methods:{
  //   updateBirth(time){
  //     this.birth = time
  //     this.$emit("changeBirth",time)
  //   }
  // }
}
</script>

