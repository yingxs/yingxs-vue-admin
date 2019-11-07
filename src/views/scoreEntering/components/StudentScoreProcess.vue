<template>
  <div class="studentScoreProcess">
    <div class="inner-process" >
      <span class="name">语文</span>
      <span class="score">100分</span>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'StudentScoreProcess'
  }
</script>

<style>
  .studentScoreProcess {
    width: 100%;
    height: 15px;
    background: #ddd;
    line-height: 15px;
    border-radius: 16px;
    margin: 2px 0px;

  }
  .studentScoreProcess .inner-process {
    display: inline-block;
    background: red;
    border-radius: 16px;
    width:100%;
    color: #fff;
    font-size: 12px;
  }

  .studentScoreProcess .inner-process .name {
    display: inline-block;
    width:48%;
    padding-left: 5px;
    text-align: left;
  }
  .studentScoreProcess .inner-process .score {
    display: inline-block;
    width:48%;
    padding-right: 5px;
    text-align: right;
  }


</style>
