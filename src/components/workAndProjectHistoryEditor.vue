<template>
  <div>
    <h3>{{title}}</h3>
    <el-form>
      <div v-for="(item,index) in items" class="one-work-history" :key="index">
        <i v-on:click="removeItem(index)" class="el-icon-close"></i>
        <el-form-item v-bind:label="labels[keys[0]] || key">
          <el-input v-model="item[keys[0]]"></el-input>
        </el-form-item>
        <el-form-item v-bind:label="labels[keys[1]] || key">
          <el-input type="textarea" v-model="item[keys[1]]" :autosize="{ minRows: 2, maxRows: 15}"></el-input>
        </el-form-item>
      </div>
      <el-button type="primary" v-on:click="addItem">再添一项</el-button>
    </el-form>
  </div>
</template>
<script>
export default {
  props: ['items','labels','title'],
  computed: {
    keys(){
      return (Object.keys(this.items[0]))
    }
  },
  methods: {
    addItem() {
      const empty = {}
      this.keys.map((key) => {
        empty[key] =''
      })
      this.items.push(empty)
    },
    removeItem(index) {
      this.items.splice(index, 1)
    }
  }
}
</script>
