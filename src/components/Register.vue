<template>
    <div  class="register-vue" :style="bg">
        <div class="container">
            <p class="title">WELCOME</p>
            <div class="input-c">
            <span>账&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;号：</span><Input  v-model="account" required placeholder="用户名" clearable />
            <p class="error">{{accountError}}</p>
            </div>
            <div class="input-c">
                <span>密&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;码：</span><Input type="password" required v-model="pwd"  placeholder="密码" clearable />
                <p class="error">{{pwdError}}</p>
            </div>
             <div class="input-c">
                <span>工作经验：</span> <Select v-model="modeljy" style="width:200px" required>
                    <Option v-for="item in cityList" :value="item.value" :key="item.value">{{ item.label }}</Option>
                </Select>
                <p class="error"></p>
             </div>
             <div class="input-c">
                <span>学&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;历：</span> <Select v-model="modelxl"  required style="width:200px">
                    <Option v-for="item in xlList" :value="item.value" :key="item.value">{{ item.label }}</Option>
                </Select>
                <p class="error"></p>
             </div>
             <div class="input-c">
                <span>擅长技术：</span> 
                <Select v-model="modeljs" multiple required  style="width:200px">
                    <Option v-for="item in jsList" :value="item.search_key" :key="item.search_key">{{ item.search_key }}</Option>
                </Select>
                <p class="error"></p>
             </div>
            <div class="input-c">
                <span>工作地点：</span> 
                <Select v-model="address" required  style="width:200px">
                    <Option v-for="item in addressList" :value="item.label" :key="item.label">{{ item.label }}</Option>
                </Select>
                <p class="error"></p>
            </div>
            <div class="input-c">
                <span>心仪职位：</span> 
                <Select v-model="major" multiple required style="width:200px">
                    <Option v-for="item in majorList" :value="item.label" :key="item.label">{{ item.label }}</Option>
                </Select>
                <p class="error"></p>
            </div>
            <Button :loading="isShowLoading" class="register" type="primary" @click="register">注册</Button>
        </div>
    </div>

</template>
<script>
export default {
  name: "register",
  data() {
    return {
      bg: {},
      account: "",
      pwd: "",
      modeljy: "",
      modelxl: "",
      modeljs: "",
      accountError: "",
      pwdError: "",
      address: "",
      major: "",
      isShowLoading: false,
      addressList: [
        {
          label: "北京"
        },
        {
          label: "上海"
        },
        {
          label: "广州"
        },
        {
          label: "深圳"
        },
        {
          label: "杭州"
        }
      ],
      cityList: [
        {
          value: "1",
          label: "1年"
        },
        {
          value: "2",
          label: "2年"
        },
        {
          value: "3",
          label: "3年"
        },
        {
          value: "4",
          label: "4年"
        },
        {
          value: "5",
          label: "5年"
        },
        {
          value: "6",
          label: "5-10年"
        }
      ],
      xlList: [
        {
          value: "0",
          label: "中专"
        },
        {
          value: "1",
          label: "大专"
        },
        {
          value: "2",
          label: "本科"
        },
        {
          value: "3",
          label: "硕士"
        },
        {
          value: "4",
          label: "博士"
        }
      ],
      majorList: [
        {
          label: "java开发工程师"
        },
        {
          label: "大数据开发工程师"
        },
        {
          label: "机器学习工程师"
        },
        {
          label: "数据分析师"
        },
        {
          label: "产品经理"
        },
        {
          label: "Android开发工程师"
        },
        {
          label: "软件测试工程师"
        },
        {
          label: "算法工程师"
        },
        {
          label: "运维工程师"
        },
        {
          label: "web前端工程师"
        },
        {
          label: "python工程师"
        },
        {
          label: "软件开发工程师"
        },
        {
          label: "项目经理"
        }
      ],
      jsList: []
    };
  },
  created() {
    this.bg.backgroundImage = "url(" + require("../assets/imgs/bg03.jpg") + ")";
  },
  methods: {
    // 擅长技术
    getGoodTech() {
      console.log(this.urlHost, "urlHost");
      this.$axios({
        url: this.urlHost + "/job/getTechTag",
        method: "get"
      }).then(res => {
        console.log(res.data.data[0].search_key, "data");
        this.jsList = res.data.data;
      });
    },
    // success tip
    success() {
      this.$Message.success("注册成功");
    },
    error () {
                this.$Message.error('注册失败');
            },
    register() {
      if (this.modeljs.length > 0) {
        this.modeljs = this.modeljs.toString();
      }
      if (this.major.length > 0) {
        this.major = this.major.toString();
      }
      this.$axios({
        url: this.urlHost + "user/register",
        method: "post",
        data: {
          telphone: this.account,
          password: this.pwd,
          techTag: this.modeljs,
          experience: this.modeljy,
          education: this.modelxl,
          cityCode: this.address,
          position: this.major
        },
        dataType: "json"
      }).then(res => {
        if (res.data.data == "注册成功") {
          this.success();
          setTimeout(()=>{this.$router.push({ path: "/login" });},1000)
          
        }
      });
    }
  },
  mounted() {
    this.getGoodTech();
  }
};
</script>
<style>
.register-vue {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
}
.register-vue .container {
  background: rgba(255, 255, 255, 0.5);
  width: 480px;
  text-align: center;
  border-radius: 10px;
  padding: 30px;
  min-height: 600px;
}
.register-vue .ivu-input {
  background-color: transparent;
  color: #fff;
  outline: #fff;
  border-color: #fff;
}
.register-vue ::-webkit-input-placeholder {
  /* WebKit, Blink, Edge */
  color: rgba(255, 255, 255, 0.8);
}
.register-vue :-moz-placeholder {
  /* Mozilla Firefox 4 to 18 */
  color: rgba(255, 255, 255, 0.8);
}
.register-vue ::-moz-placeholder {
  /* Mozilla Firefox 19+ */
  color: rgba(255, 255, 255, 0.8);
}
.register-vue :-ms-input-placeholder {
  /* Internet Explorer 10-11 */
  color: rgba(255, 255, 255, 0.8);
}
.register-vue .title {
  font-size: 16px;
  margin-bottom: 20px;
}
.register-vue .input-c {
  margin: auto;
  width: 280px;
}
.register-vue .error {
  color: red;
  text-align: left;
  margin: 5px auto;
  font-size: 12px;
  padding-left: 30px;
  height: 20px;
}
.register-vue .register {
  width: 270px;
}
.register-vue .account {
  margin-top: 30px;
}
.register-vue .account span {
  cursor: pointer;
}
.register-vue .ivu-icon {
  color: #eee;
}
.register-vue .ivu-icon-ios-close-circle {
  color: #777;
}
</style>
<style>
.ivu-select-selection {
  background-color: rgba(0, 0, 0, 0) !important;
  border: 1px solid #fff !important;
}
.ivu-select {
  color: #fff !important;
}
.ivu-select-single .ivu-select-selection .ivu-select-placeholder {
  color: #fff !important;
}
.ivu-select-multiple .ivu-select-selection .ivu-select-placeholder {
  color: #fff !important;
}
</style>
<style scoped>
.ivu-input-wrapper {
  width: 70% !important;
}
</style>



