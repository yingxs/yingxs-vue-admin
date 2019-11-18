<template>
  <div class="studentCard" >
    <el-card class="box-card" body-style="padding:20px;">
      <div slot="header" class="clearfix">
        <span>学生信息</span>
      </div>
      <el-col>
        <div class="box-center">
          <pan-thumb :image="baseInfo.s_head_image" :height="'100px'" :width="'100px'"  >
            <div>
             来了<span><br>老弟</span>
            </div>
          </pan-thumb>
        </div>
        <div class="box-center">
          <h6> {{baseInfo.s_name}} </h6>
          <h6> {{baseInfo.c_name}} </h6>
        </div>
      </el-col>

      <el-col >
        <svg-icon icon-class="education" />
        <span>查询</span>
        <hr />
      </el-col>

      <el-col :span="20" :push="2">
        <el-form @submit.native.prevent :model="numberAndScoreForm"  label-width="50px" ref="numberQueryForm" >
					<div ref="number">
						<el-form-item 
							label="学号" 
							prop="number"
							:rules="[
								{ required: true ,message: '学号不能为空' } 
							]"
						>
							<el-col  :span="18">
								<el-input   ref="inputNumber"   @keyup.enter.native.prevent="getStudentInfo"  v-model="numberAndScoreForm.number"  />
							</el-col>
							<el-col :span="3" :push="1"  >
								<el-button @click="getStudentInfo" :loading="queryLoading" type="primary">查询</el-button>
							</el-col>
						</el-form-item>
					</div>
				</el-form>
				
				<el-form  @submit.native.prevent  :model="numberAndScoreForm"  label-width="50px"  ref="scoreCommitForm"  >
          <el-form-item 
					 label="分数" 
					 prop="score"
					 :rules="[
						{ required: true ,message: '分数不能为空' },
						{ type: 'number' ,message: '分数不规范' }
					 ]"
					 >
            <el-col :span="10">
              <el-input  @keyup.enter.native="commitScore"   ref="inputScore"  v-model.number="numberAndScoreForm.score" />
            </el-col>
            <el-col :span="14" :push="2"  >
              <el-button @click="commitScore" type="primary" :loading="commitLoading"  >录入</el-button>
              <el-button @click="resetAllForm" type="primary">清空</el-button>
            </el-col>
          </el-form-item>
				</el-form>
					
					
        
      </el-col>

      <el-col >
        <svg-icon icon-class="skill" />
        <span>成绩</span>
        <hr />
      </el-col>

      <el-col :span="23" :push="2"  >
				
         <el-badge    v-for="item in socureList"   :value="item.score" class="item"> 
						<el-button size="mini">{{item.socureName  }}</el-button>
         </el-badge>
				 
				 
<!-- 
         <el-badge :value="78.56" class="item">
           <el-button size="mini">回复</el-button>
         </el-badge>

         <el-badge :value="36.45" class="item" type="primary">
           <el-button size="mini">评论</el-button>
         </el-badge>

         <el-badge :value="63.25" class="item" type="warning">
           <el-button size="mini">回复</el-button>
         </el-badge>

         <el-badge :value="98.55" class="item">
           <el-button size="mini">评论</el-button>
         </el-badge>

         <el-badge :value="78.56" class="item">
           <el-button size="mini">回复</el-button>
         </el-badge>

         <el-badge :value="36.45" class="item" type="primary">
           <el-button size="mini">评论</el-button>
         </el-badge>

         <el-badge :value="63.25" class="item" type="warning">
           <el-button size="mini">回复</el-button>
         </el-badge>
				 -->
				 
         <br /><br /><br />
      </el-col>
    </el-card>
  </div>
</template>

<script>
import PanThumb from '@/components/PanThumb'
import request from '@/utils/request'
import { MessageBox, Message } from 'element-ui'
	
	
export default {
  name: 'StudentCard',
  components: { PanThumb },
	data(){
		return {
			numberAndScoreForm: {
				number:null ,
				score: null
			},
			socureList:[
				{score: "0.00", socureName: "语文", socureId: 1},
				{score: "0.00", socureName: "数学", socureId: 1},
				{score: "0.00", socureName: "英语", socureId: 1},
				{score: "0.00", socureName: "历史", socureId: 1},
				{score: "0.00", socureName: "政治", socureId: 1},
				{score: "0.00", socureName: "物理", socureId: 1},
				{score: "0.00", socureName: "化学", socureId: 1},
				{score: "0.00", socureName: "地理", socureId: 1}
				],
			baseInfo:{
				s_name:'姓名',
				s_id: 0,
				c_name:'所属班级',
				s_head_image: 'https://wpimg.wallstcn.com/f778738c-e4f8-4870-b634-56703b4acafe.gif'
			},
			queryLoading:false,
			commitLoading:false
		}
	},
	// props:[ 'pgradeId', 'psocureId' ],
	props: {
		pgradeId: {
			type: Number
		},
		psocureId: {
			type:Number
		}
	},
	created() { },
	methods:{
		// 根据学号获得学生信息
		getStudentInfo(){
			
			
			
			this.$refs['numberQueryForm'].validate((valid) => {
				if (!valid) {
					return false;
				} else {
					if (this.queryLoading) {
						return ;
					}
					
					this.queryLoading = true;
					request({
					  url: '/student/'+this.numberAndScoreForm.number,
					  method: 'get'
					}).then(response => {
						this.queryLoading = false;
						this.baseInfo = response.data.baseInfo
						this.socureList = response.data.scoreInfo
						// 清空分数框
						this.resetScoreForm()
						// 分数框获得的焦点
						this.$refs.inputScore.focus()
					}).catch(error => {
						this.queryLoading = false
						this.clearStudentInfo()
						this.resetScoreForm()
						Message({
						  message: '学生信息查询失败：'+error.message || 'Error',
						  type: 'error',
						  duration: 5 * 1000
						})
					})
					
				}
			});
			console.log("根据学号获取学生信息");
		},
		// 清空学生信息
		clearStudentInfo(){
			this.baseInfo = {
				s_name:'姓名',
				s_id: 0,
				c_name:'所属班级',
				s_head_image: 'https://wpimg.wallstcn.com/f778738c-e4f8-4870-b634-56703b4acafe.gif'
			}
			this.socureList = [
				{score: "0.00", socureName: "语文", socureId: 1},
				{score: "0.00", socureName: "数学", socureId: 1},
				{score: "0.00", socureName: "英语", socureId: 1},
				{score: "0.00", socureName: "历史", socureId: 1},
				{score: "0.00", socureName: "政治", socureId: 1},
				{score: "0.00", socureName: "物理", socureId: 1},
				{score: "0.00", socureName: "化学", socureId: 1},
				{score: "0.00", socureName: "地理", socureId: 1} ];
		},
		// 录入成绩
		commitScore(){
			
			this.$refs['scoreCommitForm'].validate((valid) => {
				if (!valid) {
					return false;
				} else {
					if (this.pgradeId  && this.psocureId) {
						
						if (this.baseInfo.s_id == 0) {
							Message({
							  message: '请先查询出学生信息' || 'Error',
							  type: 'error',
							  duration: 3 * 1000
							})
						}

						if (this.commitLoading) {
							return ;
						}
						this.commitLoading = true;
						request({
						  url: '/score',
						  method: 'post',
							data:{
								scoGradeId:this.pgradeId,
								scoSocureId:this.psocureId,
								scoStudentId:this.baseInfo.s_id,
								scoScore:this.numberAndScoreForm.score
							}
						}).then(response => {
							this.commitLoading = false;
							
							// 成功通知弹框
							this.$notify({
								title: 'ok',
								message: response.message,
								type: 'success'
							});
							
							// 发送成功事件
							this.$emit("commitScoreSuccess");
							//  重置表单
							this.$refs.inputScore.blur()
							this.resetAllForm();
							// 学号文本框获得焦点
							this.$refs.inputNumber.focus()
							// 清空学生信息
							this.clearStudentInfo();
						}).catch(error => {
							this.commitLoading = false;
							Message({
							  message: response.message || 'Error',
							  type: 'error',
							  duration: 5 * 1000
							})
						})
						
						
						
						
						
						
						 
					} else {
						Message({
						  message: '请先选择班级和科目' || 'Error',
						  type: 'error',
						  duration: 5 * 1000
						})
					}
				}
			});
			
		},
		// 重置分数表单
		resetScoreForm() {
			this.$refs['scoreCommitForm'].resetFields();
		},
		// 重置学号表单
		resetNumberForm() {
			this.$refs['numberQueryForm'].resetFields();
		},
		resetAllForm(){
			this.resetScoreForm();
			this.resetNumberForm();
		}
		
		
		
		
	}
}
</script>

<style lang="scss" scoped>

</style>
<style>
  .foot_col {
    padding-bottom: 20px;
  }
  .item {
    margin-top: 10px;
    margin-right: 40px;
  }
  .box-center {
    margin: 0 auto;
    display: table;
  }
  .box-center h6 {
    font-size: 14px;
    margin: 0;
    padding: 0;
    text-align: center;
    font-weight: normal;
    line-height: 25px;
  }

  .studentCard label.el-form-item__label{
    font-weight: normal;
  }

  .studentCard  .el-col {
    padding: 0px !important;
    margin: 0px !important;
  }

  .studentCard hr {
    border: none;
    height: 1px;
    background: #dfe6ec;
    margin: 5px 0px 25px 0px;
  }

  /* .studentCard_body {
    padding: 10px 30px;
  } */
</style>
