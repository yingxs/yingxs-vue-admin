<template>
  <el-card>
    <div slot="header" class="clearfix">
      <span>处理进度</span>
    </div>

    <el-form label-width="50px">
        <el-col :span="20" :push="2">
          <br />
					
          <el-form-item label="班级" >
            <el-select clearable  filterable   v-model="selectGrade" :size="'small'" placeholder="请选择">
              <el-option v-for="item in gradeList" :key="item.cId" :label="item.cName" :value="item.cId"> </el-option>
            </el-select>
          </el-form-item>
					
					
          <el-form-item label="科目" >
            <el-select clearable  filterable   v-model="selectSocure" :size="'small'" placeholder="请选择">
              <el-option v-for="item in socureList" :key="item.socureId" :label="item.socureName" :value="item.socureId"> </el-option>
            </el-select>
          </el-form-item>
					
					
          <div class="box-center process-circle-charts">
            <el-progress type="circle" :percentage="processInfo.process" :width="185"  ></el-progress>
          </div>
        </el-col>
    </el-form>

      <el-form label-width="60px"  :inline="true">
        <el-col  :span="24" >
          <div class="box-center process-info">
            <el-form-item label="已处理"  >
              <el-tag :type="'success'"> {{processInfo.finish}}  </el-tag>
            </el-form-item>
            <el-form-item label="待处理"  >
              <el-tag :type="'info'">  {{processInfo.awaitDispose}}  </el-tag>
            </el-form-item>
            <el-form-item label="异常">
              <el-tag :type="'warning'">  {{processInfo.exception}} </el-tag>
            </el-form-item>
          </div>
        </el-col>
      </el-form>


  </el-card>
</template>

<script>
	import request from '@/utils/request'
	import { MessageBox, Message } from 'element-ui'
	
  export default {
    name: 'SelectAndProcessCard',
    data() {
          return {
						gradeList:[],
						selectGrade:'',
						socureList:[],
						selectSocure:''
          }
        },
				props:{
					processInfo: {
						type: Object
					}
				},
				created(){
					
					request({
					  url: '/grade/list',
					  method: 'get'
					}).then(response => {
						this.gradeList = response.data
					}).catch(error => {
						Message({
						  message: '班级列表加载失败：'+error || 'Error',
						  type: 'error',
						  duration: 5 * 1000
						})
					})
					
					request({
					  url: '/socure/list',
					  method: 'get'
					}).then(response => {
						this.socureList = response.data
					}).catch(error => {
						Message({
						  message: '课程列表加载失败：'+error || 'Error',
						  type: 'error',
						  duration: 5 * 1000
						})
					})
					
					
				},
				watch:{
					selectGrade:function(val) {
							 if (this.selectGrade != '' && this.selectSocure != '' ) {
								 // 发射事件
								 this.$emit('gradeAndSocureSelected',this.selectGrade,this.selectSocure);
							 }
					},
					selectSocure : function (val) {
							 if (this.selectGrade != '' && this.selectSocure != '' ) {
									// 发射事件
									this.$emit('gradeAndSocureSelected',this.selectGrade,this.selectSocure);
							 }
					}
				} 
  }
</script>

<style lang="scss" scoped>

</style>

<style>
  .process-info {
    padding: 20px 0px 30px 0px;
  }
  .process-circle-charts {
    padding: 23px 0px;
  }
  .el-select {
    width: 100%;
  }
</style>
