<template>
  <el-card :body-style="'padding:0'">
    <div slot="header" class="clearfix">
			<el-col :span="4">
				<span>成绩排名</span>
			</el-col>
      <el-col :span="4" :push="15">
				<el-switch  active-text="同分同位"  
					@change="switchChange"
					v-model="equalScoreRankEqueal" 
					active-value="1"  
					inactive-value="0" 
					active-color="#13ce66" 
					inactive-color="#a0a0a0" > 
				</el-switch>
			</el-col>
    </div>
    <el-table   :data="ptableData" v-loading="plistLoading" height="500"  border style="width: 100%; border: none;">
      <el-table-column prop="rank" label="名次" width="50">  </el-table-column>
      <el-table-column prop="sName" label="姓名" width="120">  </el-table-column>
      <el-table-column  prop="scoScore"  label="本科成绩" width="100"> </el-table-column>
			
<!--
      <el-table-column prop="otherScore" label="其他成绩"  width="150">
         <student-score-process ></student-score-process>
         <student-score-process ></student-score-process>
         <student-score-process ></student-score-process>
         <student-score-process ></student-score-process>
         <student-score-process ></student-score-process>
         <student-score-process ></student-score-process>
         <student-score-process ></student-score-process>
         <student-score-process ></student-score-process>
       </el-table-column>
 -->
      <el-table-column label="操作"  width="205">
        <template slot-scope="scope">
          <el-button type="primary" icon="el-icon-edit" size="small">修改</el-button>
          <el-button type="danger" icon="el-icon-delete" size="small">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </el-card>
</template>


<script>
  import StudentScoreProcess from './StudentScoreProcess'
  export default {
    methods: {
      handleClick(row) {
        console.log(row);
      }
    },
    components:{StudentScoreProcess},

    data() {
      return {
				equalScoreRankEqueal:'1'
      }
    },
		methods: {
			switchChange(value){
				 this.$emit('switchChange',value)
			}
		},
		props: {
			plistLoading: {
				type: Boolean
			},
			ptableData: {
				type:Array
			}
		}  
  }
</script>
<style>

.gutter {
  display: none;
}
</style>
