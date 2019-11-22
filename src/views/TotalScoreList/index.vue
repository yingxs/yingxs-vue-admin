<template>
	<div class="app-container">
		<div class="filter-container">
			
			<el-select clearable  filterable   v-model="selectGrade" style="width: 200px;"  class="filter-item" placeholder="班级">
				<el-option v-for="item in gradeList" :key="item.cId" :label="item.cName" :value="item.cId"> </el-option>
			</el-select>
			
			<el-input  placeholder="姓名" style="width: 200px;" class="filter-item"   />
			<el-button  @click="listLoad" class="filter-item" type="primary" icon="el-icon-search"  >
			  Search
			</el-button>
			<el-button   class="filter-item" type="primary" icon="el-icon-download"  >
			  Export
			</el-button>
		</div>
		<el-table v-loading="loading"  :data="paging.listData" >
			 <el-table-column align="center" prop="rank" label="全校排名" width="80" />
			 <el-table-column align="center" prop="studentName" label="姓名" width="180" />
			 <el-table-column align="center" prop="gradeName" label="班级" width="180" />
			<el-table-column align="center" v-for="column in tableData.columns" :key="column.soId" :label="column.soName">
				<template slot-scope="scope">
					<span> {{scope.row.studentMultipleMap[column.soField]  }} </span>
				</template>
			</el-table-column>
			<el-table-column align="center" prop="totalScore" label="总分" width="180" />
			<el-table-column  align="center"  label="操作"  width="205">
					<template slot-scope="{row}">
						
					   
						
					  <el-button
					    type="primary"
					    size="small"
					    icon="el-icon-edit"
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
		<pagination v-show="paging.total>0" :total="paging.total" :page.sync="paging.page" :limit.sync="paging.pageSize" @pagination="getPageList" />
	</div>
</template>

<script>
import request from '@/utils/request'
import { MessageBox, Message } from 'element-ui'
import Pagination from '@/components/Pagination'


export default {
  name: 'TotalScoreList',
	components:{ Pagination },
	data(){
		return {
			gradeList:[],
			selectGrade:'',
			socureList:[],
			selectSocure:'',
			tableData:{},
			loading:false,
			paging : {
				listData:[],
				total:0,
				page:1,
				pageSize:10
				
			}
			
		}
	},
	created() {
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
		});
		
		this.listLoad()
	},
	methods: {
		getPageList(){
			this.paging.listData = []
			for (let i = ( (this.paging.page-1) * this.paging.pageSize ) ; i < this.paging.pageSize + ( (this.paging.page-1) * this.paging.pageSize ) ; i++ ) {
				if (this.tableData.scoreList[i] == undefined) {
					break 
				}
				this.paging.listData.push(this.tableData.scoreList[i]);
			}
		},
		listLoad(){
			this.loading = true;
			request({
			  url: '/score/gradeList',
			  method: 'get',
				params: {
					gradeId:this.selectGrade,
					equalScoreRankEqueal:0
				}
			}).then(response => {
				this.loading = false;
				this.tableData = response.data
				
				
				this.paging.total = this.tableData.scoreList.length
				this.getPageList()
			}).catch(error => {
				this.loading = false;
				Message({
				  message: '成绩列表加载失败：'+error || 'Error',
				  type: 'error',
				  duration: 5 * 1000
				})
			});
		}
	}
	
}
</script>

<style>
</style>
