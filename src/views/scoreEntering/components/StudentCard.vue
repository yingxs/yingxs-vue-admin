<template>
  <div class="studentCard" >
    <el-card class="box-card" body-style="padding:20px;">
      <div slot="header" class="clearfix">
        <span>信息查询3</span>
      </div>

      <el-col>
        <div class="box-center">
          <pan-thumb :image="'https://wpimg.wallstcn.com/f778738c-e4f8-4870-b634-56703b4acafe.gif'" :height="'100px'" :width="'100px'"  >
            <div>
             来了<span><br>老弟</span>
            </div>
          </pan-thumb>
        </div>
        <div class="box-center">
          <h6>刘畅</h6>
          <h6>三年级二班</h6>
        </div>
      </el-col>

      <el-col >
        <svg-icon icon-class="education" />
        <span>查询</span>
        <hr />
      </el-col>

      <el-col :span="20" :push="2">
        <el-form label-width="40px">
          <el-form-item label="编号">
            <el-input />
          </el-form-item>
          <el-form-item label="条件">
            <el-col :span="10">
              <el-input />
            </el-col>
            <el-col :span="6" :push="3">
              <el-button type="primary">查询</el-button>
            </el-col>
          </el-form-item>
        </el-form>
      </el-col>

      <el-col >
        <svg-icon icon-class="skill" />
        <span>进度</span>
        <hr />
      </el-col>

      <el-col :span="23" :push="1">
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
      </el-col>

    </el-card>
  </div>
</template>

<script>
import PanThumb from '@/components/PanThumb'

export default {
  name: 'StudentCard',
  components: { PanThumb }
}
</script>

<style lang="scss" scoped>

</style>
<style>
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
