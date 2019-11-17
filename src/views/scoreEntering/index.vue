<template>
  <div class="app-container">
    <el-row :gutter="20">
      <el-col :span="6" :xs="24">
        <select-and-process-card  @gradeAndSocureSelected="gradeAndSocureSelected" />
      </el-col>
     <el-col :span="7" :xs="24">
       <student-card :pgrade-id="gradeId"  :psocure-id="socureId"  />
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

export default {
  name: 'ScoreEntering',
  components: { UserCard, StudentCard,SelectAndProcessCard,StudentSingleScoreList },
  data() {
    return {
			gradeId: 0,
			socureId: 0,
			listLoading:false,
			equalScoreRankEqueal:'0',
			tableData:[]
		}
  },
	methods: {
		gradeAndSocureSelected(gradeId,socureId){
			 this.gradeId = gradeId
			 this.socureId = socureId
			 
			 console.log("gradeAndSocureSelected")
			 
			 request({
			   url: '/score/list',
			   method: 'get',
			 	params: {
			 		gradeId:gradeId,
			 		sourceId:gradeId,
			 		equalScoreRankEqueal:this.equalScoreRankEqueal
			 	}
			 }).then(response => {
			 	this.tableData = response.data
			 }).catch(error => {
			 	Message({
			 	  message: '班级单科排名查询失败：'+error.message || 'Error',
			 	  type: 'error',
			 	  duration: 5 * 1000
			 	})
			 })
		},
		switchChange(value){
			this.equalScoreRankEqueal = value;
		}
	}
}
</script>
<style>
</style>
