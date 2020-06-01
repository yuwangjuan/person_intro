<template>
    <div  class="register-vue" :style="bg">
        <div class="container">
            <p class="title">WELCOME</p>
            <div class="input-c">
            <span>账&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;号：</span><Input  v-model="account" placeholder="用户名" clearable @on-blur="verifyAccount"/>
            <p class="error">{{accountError}}</p>
            </div>
            <div class="input-c">
                <span>密&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;码：</span><Input type="password" v-model="pwd"  placeholder="密码" clearable @on-blur="verifyPwd"/>
                <p class="error">{{pwdError}}</p>
            </div>
             <div class="input-c">
                <span>工作经验：</span> <Select v-model="model1" style="width:200px">
                    <Option v-for="item in cityList" :value="item.value" :key="item.value">{{ item.label }}</Option>
                </Select>
                <p class="error"></p>
             </div>
             <div class="input-c">
                <span>学&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;历：</span> <Select v-model="model3" style="width:200px">
                    <Option v-for="item in xlList" :value="item.value" :key="item.value">{{ item.label }}</Option>
                </Select>
                <p class="error"></p>
             </div>
             <div class="input-c">
                <span>擅长技术：</span> <Select v-model="model2" multiple  style="width:200px">
                    <Option v-for="item in jsList" :value="item.value" :key="item.value">{{ item.label }}</Option>
                </Select>
                <p class="error"></p>
             </div>
             <div class="input-c">
                <span>工作地点：</span><Input type="text" v-model="address"  placeholder="工作地点偏好" clearable @on-blur="verifyPwd"/>
                <p class="error"></p>
            </div>
            <div class="input-c">
                <span>心仪职位：</span><Input type="text" v-model="major"  placeholder="心仪职位" clearable @on-blur="verifyPwd"/>
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
      bg:{},
      account:'',
      pwd:'',
      model1:'',
      model2:'',
      model3:'',
      accountError:'',
      pwdError:'',
      address:'',
      major:'',
      isShowLoading:false,
      cityList:[
        {
                        value: '1年',
                        label: '1年'
                    },
                    {
                        value: '2年',
                        label: '2年'
                    },
                    {
                        value: '3年',
                        label: '3年'
                    },
                    {
                        value: '4年',
                        label: '4年'
                    },
                    {
                        value: '5年',
                        label: '5年'
                    },
                    {
                        value: '5-10年',
                        label: '5-10年'
                    }
      ],
      xlList:[
        {
                        value: '大专',
                        label: '大专'
                    },
                    {
                      value: '本科',
                        label: '本科'
                    },
                    {
                      value: '硕士',
                        label: '硕士'
                    },
                    {
                      value: '博士',
                        label: '博士'
                    },
      ],
      jsList:[
        {
                        value: 'java',
                        label: 'java'
                    },
                    {
                      value: 'javascript',
                        label: 'javascript'
                    },
                    {
                      value: 'c+',
                        label: 'c+'
                    },
                    {
                      value: 'python',
                        label: 'python'
                    },
      ]

    }
  },
  created() {
        this.bg.backgroundImage = 'url(' + require('../assets/imgs/bg03.jpg') + ')'
    },
    methods:{
      verifyAccount() {
            var uPattern = /^[a-zA-Z0-9_]{4,16}$/;
            if ( uPattern.test(this.account)==false) {
                this.accountError = '4-16位(字母,数字,下划线)'
            } else {
                this.accountError = ''
            }
        },
        verifyPwd() {
            if (this.pwd !== 'admin') {
                // this.pwdError = '密码为admin'
                this.pwdError = ''
            } else {
                this.pwdError = ''
            }
        },
        register() {
          this.$router.push({path:'/login'})
        }
    }
}
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
  height:600px;
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
.ivu-select-selection{
  background-color:rgba(0,0,0,0) !important;
  border:1px solid #fff !important;
  
}
.ivu-select{
  color:#fff !important;
}
.ivu-select-single .ivu-select-selection .ivu-select-placeholder{
color:#fff !important;
}
.ivu-select-multiple .ivu-select-selection .ivu-select-placeholder{
  color:#fff !important;
}
</style>
<style scoped>
.ivu-input-wrapper{
  width:70% !important;
}
</style>



