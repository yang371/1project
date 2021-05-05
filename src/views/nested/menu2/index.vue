<template>
  <div class="menu" style="text-align: center">

    <el-menu
      :default-active="activeIndex2"
      class="el-menu-demo"
      mode="horizontal"
      @select="handleSelect"
      background-color="rgba(0,0,0,0.2)"
      text-color="#fff"
      active-text-color="rgba(0,0,0,0.2)" >

      <el-submenu index="1"  >
        <template slot="title"  class="el-menu1-demo">设备选择</template>
        <el-menu-item index="1-1">液晶显示屏</el-menu-item>
        <el-menu-item index="1-2">数字像源</el-menu-item>
        <el-menu-item index="1-3">平显设备与头显设备</el-menu-item>
      </el-submenu>

      <el-submenu index="3" >
        <template slot="title" class="menu2">在线诊断</template>
        <el-menu-item index="3-1">选项1</el-menu-item>
        <el-menu-item index="3-2">选项2</el-menu-item>
        <el-menu-item index="3-3">选项3</el-menu-item>
      </el-submenu>



      <el-submenu index="4" >
        <template slot="title" class="menu2">信息管理</template>
        <el-menu-item index="4-1">选项1</el-menu-item>
        <el-menu-item index="4-2">选项2</el-menu-item>
        <el-menu-item index="4-3">选项3</el-menu-item>
      </el-submenu>


    </el-menu>
    <div class="line">1</div>
    <div class="text">
      <span>设备选择</span>
      <el-divider direction="vertical"></el-divider>
      <span>在线诊断</span>
      <el-divider direction="vertical"></el-divider>
      <span>信息管理</span>
    </div>
    <div class="select">
      搜索：
        <el-select v-model="value" placeholder="请选择"
                    style="width: 580px" >
          <el-option-group
            style="width: 580px"
            v-for="group in options"
            :key="group.label"
            :label="group.label">
            <el-option
              style="width: 580px"
              v-for="item in group.options"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-option-group>
        </el-select>




    </div>
  </div>

</template>
<script>
  export default {
    data() {
      return {
        options: [{
          label: '热门城市',
          options: [{
            value: 'Shanghai',
            label: '上海'
          }, {
            value: 'Beijing',
            label: '北京'
          }]
        }, {
          label: '城市名',
          options: [{
            value: 'Chengdu',
            label: '成都'
          }, {
            value: 'Shenzhen',
            label: '深圳'
          }, {
            value: 'Guangzhou',
            label: '广州'
          }, {
            value: 'Dalian',
            label: '大连'
          }]
        }],
        value: ''
      }
    }
  }
</script>
<style >
  body{
    /*background-image:url('../../../assets/background.jpg') no-repeat -10px 0;*/
    background:url(assets/background.jpg) no-repeat -350px -350px;
opacity: 1;
  }
  .menu{

    filter:alpha(opacity=60);

    width:100%;
    position:absolute;

    background-attachment:fixed;


  }
  .el-menu--horizontal .el-menu--popup .el-menu-item {
    height: 50px;
    line-height: 30px;
    width:500px;
    font-size: 20px;
  }
  .el-menu-demo{
    left: 0px;
    width:2100px;
    font-size:100px;
    opacity: 1;
  }
  .el-menu--horizontal>.el-submenu .el-submenu__title {
    height: 60px;
    line-height: 60px;
    width:500px;
    border-bottom: 2px solid transparent;
    color: rgba(0,0,0,0.2);
    font-size: 20px;
    opacity: 1;
  }
  .line{
    background:url(assets/background.jpg);
    position:absolute;
    width:2000px;
    margin-top:-1px;
    height: 0.5px;
  }

.select{
  position:absolute;
  margin-top:330px;
  margin-left:500px;
  color:white;
  font-size: 23px;
}
  .text{
    position:absolute;
    margin-top:260px;
    margin-left:710px;
    color:white;
    font-size: 23px;
  }


</style>
