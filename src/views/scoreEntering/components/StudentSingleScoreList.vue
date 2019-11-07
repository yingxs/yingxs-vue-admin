<template>
  <el-card :body-style="'padding:0'">
    <div slot="header" class="clearfix">
      <span>成绩排名</span>
    </div>
    <el-table :data="tableData" height="500"  border style="width: 100%; border: none;">
      <el-table-column prop="rank" label="名次" width="50">  </el-table-column>
      <el-table-column prop="name" label="姓名" width="120">  </el-table-column>
      <el-table-column  prop="currScore"  label="本科成绩" width="100"> </el-table-column>
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
        tableData: [{
          rank:1,
          name: '王小虎',
          currScore: '26.35',
          otherScore: '65',
        },
        {
          rank:2,
          name: '王小虎',
          currScore: '26.35',
          otherScore: '65',
        },
        {
          rank:2,
          name: '王小虎',
          currScore: '26.35',
          otherScore: '65',
        },{
          rank:2,
          name: '王小虎',
          currScore: '26.35',
          otherScore: '65',
        },{
          rank:2,
          name: '王小虎',
          currScore: '26.35',
          otherScore: '65',
        },{
          rank:2,
          name: '王小虎',
          currScore: '26.35',
          otherScore: '65',
        },{
          rank:2,
          name: '王小虎',
          currScore: '26.35',
          otherScore: '65',
        },{
          rank:2,
          name: '王小虎',
          currScore: '26.35',
          otherScore: '65',
        },{
          rank:2,
          name: '王小虎',
          currScore: '26.35',
          otherScore: '65',
        },{
          rank:2,
          name: '王小虎',
          currScore: '26.35',
          otherScore: '65',
        },{
          rank:2,
          name: '王小虎',
          currScore: '26.35',
          otherScore: '65',
        },{
          rank:2,
          name: '王小虎',
          currScore: '26.35',
          otherScore: '65',
        }
        ]
      }
    }
  }
</script>
<style>

.gutter {
  display: none;
}
</style>
