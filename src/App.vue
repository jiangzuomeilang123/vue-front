<template>
  <div>
    <ul>
      <li v-for="item in list" :key="item.id">abc{item.id}}:{{item.name}}</li>
    </ul>

    <el-form
      label-position="right"
      label-width="100px"
      :model="ruleForm"
      :rules="rules"
      ref="ruleForm"
    >
      <el-row v-for="(item, index) in formData" :key="index">
        <el-col>
          <el-form-item :label="item.name">
            <template v-if="item.type === 'input'">
              <el-input :placeholder="item.name"></el-input>
            </template>
            <template v-if="item.type === 'select'">
              <el-select :placeholder="item.name"></el-select>
            </template>
            <template v-if="item.type === 'radio'">
              <el-radio :placeholder="item.name"></el-radio>
            </template>
            <template v-if="item.type === 'date'">
              <el-date-picker
                :editable="false"
                type="date"
                format="yyyy-MM-dd"
                :placeholder="item.name"
              ></el-date-picker>
            </template>
          </el-form-item>
        </el-col>
      </el-row>
    </el-form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'app',
  data() {
    return {
      list: [],
      formData: [],
      ruleForm: {},
      rules: {}
    }
  },
  mounted() {
    axios.get('/api/list').then(response => {
      this.list = response.data || []
    })
    axios.get('/api/test').then(response => {
      this.formData = response.data || []
    })
  }
}
</script>

<style>
</style>
