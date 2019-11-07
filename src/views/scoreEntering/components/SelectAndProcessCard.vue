<template>
  <el-card>
    <div slot="header" class="clearfix">
      <span>处理进度</span>
    </div>

    <el-form label-width="50px">
        <el-col :span="20" push="2">
          <br />
          <el-form-item label="选择1" >
            <el-select  v-model="value" :size="'small'" placeholder="请选择">
              <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.label"
                :value="item.value">
              </el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="选择2" >
            <el-select  v-model="value" :size="'small'" placeholder="请选择">
              <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.label"
                :value="item.value">
              </el-option>
            </el-select>
          </el-form-item>
          <div class="box-center process-circle-charts">
            <el-progress type="circle" :percentage="10" width="185"  ></el-progress>
          </div>
        </el-col>
    </el-form>

      <el-form label-width="60px"  inline="true">
        <el-col  :span="24" >
          <div class="box-center process-info">
            <el-form-item label="已处理"  >
              <el-tag :type="'success'"> 26  </el-tag>
            </el-form-item>
            <el-form-item label="待处理"  >
              <el-tag :type="'info'"> 20  </el-tag>
            </el-form-item>
            <el-form-item label="异常">
              <el-tag :type="'warning'"> 0  </el-tag>
            </el-form-item>
          </div>
        </el-col>
      </el-form>


  </el-card>
</template>

<script>
  export default {
    name: 'SelectAndProcessCard',
    data() {
          return {
            options: [{
              value: '选项1',
              label: '黄金糕'
            }, {
              value: '选项2',
              label: '双皮奶'
            }, {
              value: '选项3',
              label: '蚵仔煎'
            }, {
              value: '选项4',
              label: '龙须面'
            }, {
              value: '选项5',
              label: '北京烤鸭'
            }],
            value: ''
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
