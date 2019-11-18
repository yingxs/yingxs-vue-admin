<template>
  <div class="app-container">
    <el-row :gutter="20">
      <el-col :span="6" :xs="24">
        <select-and-process-card  :processInfo="processInfo"  @gradeAndSocureSelected="gradeAndSocureSelected" />
      </el-col>
     <el-col :span="7" :xs="24">
       <student-card :pgrade-id="gradeId"  :psocure-id="socureId" @commitScoreSuccess="commitScoreSuccess"  />
     </el-col>
     <el-col :span="10" :xs="24">
        <student-single-score-List  @switchChange="switchChange"  :plistLoading="listLoading"  :ptableData="tableData"    />
     </el-col>

    </el-row>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import UserCard from '../profile/components/UserCard'
import StudentCard from './components/StudentCard'
import SelectAndProcessCard from './components/SelectAndProcessCard'
import StudentSingleScoreList from './components/StudentSingleScoreList'
import request from '@/utils/request'

export default {
  name: 'ScoreEntering',
  components: { UserCard, StudentCard,SelectAndProcessCard,StudentSingleScoreList },
  data() {
    return {
			gradeId: 0,
			socureId: 0,
			listLoading:false,
			equalScoreRankEqueal:'1',
			tableData:[],
			processInfo:{
				process:0,
				finish:0,
				awaitDispose:0,
				exception:0,
			}
		}
  },
	methods: {
		gradeAndSocureSelected(gradeId,socureId){
			 this.gradeId = gradeId
			 this.socureId = socureId
			 this.getGradeProcess({gradeId:this.gradeId,socureId:this.socureId});
			 this.commitScoreSuccess()
		},
		commitScoreSuccess(){
			this.listLoading = true
			request({
			  url: '/score/list',
			  method: 'get',
				params: {
					gradeId:this.gradeId,
					sourceId:this.socureId,
					equalScoreRankEqueal:this.equalScoreRankEqueal
				}
			}).then(response => {
				this.listLoading = false
				// 刷新排名列表
				this.tableData = response.data
				// 刷新录入进度
				this.getGradeProcess({gradeId:this.gradeId,socureId:this.socureId});
				
			}).catch(error => {
				this.listLoading = false
				Message({
				  message: '班级单科排名查询失败：'+error.message || 'Error',
				  type: 'error',
				  duration: 5 * 1000
				})
			});
		},
		getGradeProcess(query){
			request({
			  url: '/score/process',
			  method: 'get',
				params:query
			}).then(response => {
				this.processInfo = response
			}).catch(error => {
				Message({
				  message: '录入进度加载失败：'+error || 'Error',
				  type: 'error',
				  duration: 5 * 1000
				})
			})
		},
		switchChange(value){
			this.equalScoreRankEqueal = value
			this.commitScoreSuccess()
		}
	}
}
</script>
<style>
</style>
