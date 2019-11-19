<template>
  <el-card :body-style="'padding:0'">
    <div slot="header" class="clearfix">
			<el-col :span="4">
				<span>成绩排名</span>
			</el-col>
      <el-col :span="5" :push="15">
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
      <el-table-column align="center"   label="名次" width="50">
				<template slot-scope="scope">
				  <span>{{ scope.row.rank }}</span>
				</template>
			</el-table-column>
      <el-table-column align="center"   label="姓名" width="120">
				<template slot-scope="scope">
				  <span>{{ scope.row.sName }}</span>
				</template>
			</el-table-column>
      <el-table-column   align="center"   label="本科成绩" width="200">
				<template slot-scope="{row}">
				  <template v-if="row.edit">
						<el-col :span="13">
							<el-input v-model="row.assistantScoScore" class="edit-input" size="small" />
						</el-col>
						<el-col :span="2">
							<el-button
							  class="cancel-btn"
							  size="small"
							  icon="el-icon-refresh"
							  type="warning"
							  @click="cancelEdit(row)"
							>取消</el-button>
						</el-col>
				  </template>
				  <span v-else>{{ row.scoScore }}</span>
				</template>
			</el-table-column>
      <el-table-column  align="center"  label="操作"  width="205">
					<template slot-scope="{row}">
						
					  <el-button
					    v-if="row.edit"
					    type="success"
					    size="small"
					    icon="el-icon-circle-check-outline"
					    @click="confirmEdit(row)"
					  >确认</el-button>
						
					  <el-button
					    v-else
					    type="primary"
					    size="small"
					    icon="el-icon-edit"
					    @click="row.edit = !row.edit"
					  >修改</el-button>
						
						<el-button
						  type="danger"
						  size="small"
						  icon="el-icon-delete" 
							@click="deleteScore(row)"
						>删除</el-button>
						
					</template>
      </el-table-column>
    </el-table>
  </el-card>
</template>


<script>
  import StudentScoreProcess from './StudentScoreProcess'
	import request from '@/utils/request'
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
			},
			confirmEdit(row) {
				this.$emit('loadingList')
				row.scoScore = row.assistantScoScore
				request({
				  url: '/score',
				  method: 'PATCH',
					data: row
				}).then(response => {
					// 成功通知弹框
					this.$notify({
						title: 'ok',
						message: response.message,
						type: 'success'
					})
					// 刷新列表
					this.$emit('updateList')
					
				}).catch(error => {
					this.$emit('unLoadingList')
					Message({
					  message: '修改成绩失败：'+error || 'Error',
					  type: 'error',
					  duration: 5 * 1000
					})
				})
				
			},
			cancelEdit(row) {
				row.assistantScoScore = row.scoScore
				row.edit = false;
			},
			deleteScore(row){
				this.$confirm('确认删除【'+row.sName+'】的成绩吗', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
					
          this.$emit('loadingList')
          request({
            url: `/score/${row.scoId}`,
            method: 'DELETE'
          }).then(response => {
          	// 成功通知弹框
          	this.$notify({
          		title: 'ok',
          		message: response.message,
          		type: 'success'
          	})
          	// 刷新列表
          	this.$emit('updateList')
          }).catch(error => {
          	this.$emit('unLoadingList')
          	Message({
          	  message: '删除失败：'+error || 'Error',
          	  type: 'error',
          	  duration: 5 * 1000
          	})
          })
					
        }).catch(() => {
					 this.$notify({
					 	title: '取消',
					 	message: '已取消删除',
					 	type: 'info'
					 })
        });
				
				
				
				
				
				
				
				
				
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
