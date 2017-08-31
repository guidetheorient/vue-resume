<template>
  <div>
    <h2>学习经历</h2>
    <el-form>
      <div v-for="(item,index) in items" class="one-work-history">
        <i v-on:click="removeItem(index)" class="el-icon-close"></i>
        <el-form-item label="学校">
          <el-input v-model="items.school"></el-input>
        </el-form-item>
        <el-form-item label="学历">
          <el-input v-model="items.degree"></el-input>
        </el-form-item>
        <el-form-item label="时间">
          <el-input v-model="items.duration"></el-input>
        </el-form-item>
      </div>
      <el-button type="primary" v-on:click="addItem">添加</el-button>
    </el-form>
  </div>
</template>
<script>
export default {
  props: ["items"],
  methods: {
    addItem() {
      this.items.push({
        school:'',degree:'',duration:''
      })
    },
    removeItem(index) {
      this.items.splice(index, 1)
    }
  }
}
</script>