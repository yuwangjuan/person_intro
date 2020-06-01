<template>
    <div class="home-container">
        <div class="home-content">
            <div class="ipt">
                <input type="text"  class="ipt-text" placeholder="智能搜索"/>
                <Icon type="ios-search"  class="icon-search"/>
            </div>
            <div class="main-content">
                <div class="contain-left">
                    <p class="hot-refer">热门推荐</p>
                    <Tabs type="card">
        <TabPane label="杭州">
            <div class="add-scroll">
            <div class="card-box">
               <p class="title">大数据开发工程师</p>
               <p>base 杭州</p>
               <p>薪资 25-40k</p>
               <p>要求：熟悉Hadoop,spark,cdh,java,flink</p>
               <p>杭州网易云有限公司</p>
            </div>
            <div class="card-box">
               <p class="title">人工智能</p>
               <p>base 杭州</p>
               <p>薪资 23-50k</p>
               <p>要求：精通数据挖掘，深度学习算法，精通sql及电商业务。</p>
               <p>杭州阿里巴巴有限公司</p>
            </div>
            <div class="card-box">
               <p class="title">java</p>
               <p>base 杭州</p>
               <p>薪资 10-20k</p>
               <p>要求：熟练操作mysql数据库</p>
               <p>杭州海康威视有限公司</p>
            </div>
            </div>
        </TabPane>
        <TabPane label="北京">
            <div class="card-box">
               <p class="title">java</p>
               <p>base 北京</p>
               <p>薪资 10-20k</p>
               <p>要求：熟练操作mysql数据库</p>
               <p>杭州达达有限公司</p>
            </div>
        </TabPane>
        <TabPane label="广州">标签二的内容</TabPane>
        <TabPane label="上海">标签三的内容</TabPane>
    </Tabs>
                </div>
                  <div class="contain-center">
                    <p class="hot-refer">热门推荐</p>
                   
                 <div class="add-scroll">
                 </div>
                </div>
                <!-- right -->
                <div class="contain-right">
                    <p class="hot-refer">个性化推荐</p>
            <div class="add-scroll">
            <div class="card-box">
               <p class="title">java</p>
               <p>base 杭州</p>
               <p>薪资 15-25k</p>
               <p>要求：985/211本科以上学历;熟悉软件开发；软件测试等流程</p>
               <p>浙江联通股份有限公司</p>
            </div>
            <div class="card-box">
               <p class="title">java</p>
               <p>base 杭州</p>
               <p>薪资 10-20k</p>
               <p>要求：微服务/DEVOPS相关经验;精通JAVA;熟悉金融相关业务</p>
               <p>杭州同盾科技有限公司</p>
            </div>
            </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: "tuijian"
};
</script>

<style scoped>
.home-container {
  padding: 10px;
  padding-top: 5px;
  /* background:url('../assets/imgs/02.jpg') no-repeat center center;
  background-size:100% 100%; */
}
.home-content {
  padding: 10px;
  border-radius: 5px;
  
  /* background: #fff; */
}
.ipt {
  width: 50%;
  margin: 0 auto;
  height: 70px;
}
.ipt-text {
  width: 100%;
  height: 48px;
  border-radius: 100px;
  border-color: #2d89f9;
  border-style: solid;
  background: #093060;
  color: #fff;
  line-height: 48px;
  padding-left: 20px;
  display: inline-block;
}
.icon-search {
  width: 100px;
  height: 48px;
  display: inline-block;
  margin-top: -48px;
  position: absolute;
  right: 25%;
  color: #fff;
  font-size: 25px;
  line-height: 48px;
}
.main-content {
  width: 100%;
  height: 600px;
  /* border:1px solid #afa; */
}
.contain-left {
  width: 30%;
  display:inline-block;
  /* height:500px; */
  /* border:1px solid red; */
}
.contain-center{
    width:40%;
    height: 600px;
    vertical-align:top;
    /* border:1px solid red; */
    display:inline-block;
    /* border:1px solid grey; */
}
.contain-right{
    width:29%;
    display:inline-block;
    /* border: 1px solid yellow; */
    vertical-align: top;
}
.hot-refer {
  color: #fff;
  font-size: 26px;
  margin-bottom: 10px;
  text-align:center;
}
.add-scroll {
    height:700px;
   overflow-y:auto;
    /*overflow-y:scroll; */
}
.card-box {
  width: 100%;
  height: 200px;
  margin: 0 auto;
  /* border: 1px dashed #fff; */
  background: rgba(56, 76, 93, 0.2);
  color: #fff;
  padding: 15px;
  margin-top: 10px;
}
</style>
<style>
input {
  outline-color: invert;
  outline-style: none;
  outline-width: 0px;
  border-style: none;
  text-shadow: none;
  -webkit-appearance: none;
  -webkit-user-select: text;
  outline-color: transparent;
  box-shadow: none;
}
.ivu-tabs-bar {
  border-bottom: none !important;
}
.ivu-tabs.ivu-tabs-card > .ivu-tabs-bar .ivu-tabs-tab-active {
  background: #dc5e44 !important;
  border-color: none !important;
  color: #fff !important;
  outline: none;
  border-style: none;
}
.ivu-tabs.ivu-tabs-card > .ivu-tabs-bar .ivu-tabs-tab {
  background: none;
  border: 1px solid #e46243;
  width: 65px;
  color: #e46243;
  margin-right: 0px;
  border-radius: 0px;
}
.ivu-tabs-nav-container:focus .ivu-tabs-tab-focused {
  border-color: none !important;
}
  /* .add-scroll {
  width : 30px;
  height: 300px;
  margin: 0 auto;
  }
  .add-scroll::-webkit-scrollbar {
  /*滚动条整体样式*/
  /* width : 10px;  /*高宽分别对应横竖滚动条的尺寸*/
  /* height: 1px;
  } */
    .add-scroll::-webkit-scrollbar-thumb {
  /*滚动条里面小方块*/
  border-radius: 10px;
  box-shadow   : inset 0 0 5px rgba(0, 0, 0, 0.2);
  background   : #535353;
  }
  .content-left::-webkit-scrollbar-track {
  /*滚动条里面轨道*/
  box-shadow   : inset 0 0 5px rgba(0, 0, 0, 0.2);
  border-radius: 10px;
  background   : #ededed;
  } 
</style>




