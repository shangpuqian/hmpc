<template>
  <div class="login">
    <div class="login_background">
      <div class="box">
        <div class="header">
          <img src="~@/assets/logo_index.png" alt="">
        </div>
        <el-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm">
            <el-form-item prop="mobile">
              <el-input placeholder="请输入手机号" v-model.number="ruleForm.mobile" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item prop="code">
              <el-input placeholder="请输入验证码" v-model.number="ruleForm.code" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item prop="ischecked">
              <a href="javascript:;">
               <el-checkbox v-model="ruleForm.ischecked" label="我已阅读用户协议和隐藏条款"></el-checkbox>
              </a>
            </el-form-item>
            <el-form-item>
              <el-button type="primary" @click="submitForm('ruleForm')">登录</el-button>
            </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'login',
  data () {
    var checkmobile = (rule, value, callback) => {
      if (!value) {
        return callback(new Error('手机号不能为空'))
      }
      setTimeout(() => {
        var Regex = /^(0|86|17951)?(13[0-9]|15[012356789]|166|17[3678]|18[0-9]|14[57])[0-9]{8}$/
        if (!Regex.test(value)) {
          callback(new Error('请输入正确的手机号'))
        } else {
          callback()
        }
      }, 500)
    }
    var checkcode = (rule, value, callback) => {
      if (!value) {
        return callback(new Error('验证码不能为空'))
      }
      setTimeout(() => {
        var Regex = /^\d{6}$/
        if (!Regex.test(value)) {
          callback(new Error('请输入正确的验证码'))
        } else {
          callback()
        }
      }, 500)
    }
    var checkischecked = (rule, value, callback) => {
      if (!value) {
        callback(new Error('请阅读用户协议和隐私条款'))
      }
    }
    return {
      ruleForm: {
        mobile: '',
        code: '',
        ischecked: ''
      },
      rules: {
        mobile: [
          { validator: checkmobile, trigger: ['blur'] }
        ],
        code: [
          { validator: checkcode, trigger: ['blur'] }
        ],
        ischecked: [
          { validator: checkischecked, trigger: ['change'] }
        ]
      }
    }
  },
  methods: {
    submitForm (formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert('submit!')
        } else {
          console.log('error submit!!')
          return false
        }
      })
    }
  }
}
</script>

<style lang='less' scoped>
.login_background {
  width: 100vw;
  height: 100vh;
  background: url("~@/assets/login_bg.jpg") no-repeat;
  background-size: cover;
  display: flex;
  justify-content: center;
  align-items: center;
  .box {
    width: 400px;
    height: 380px;
    background-color: #fff;
    padding: 20px;
    .header {
      padding-bottom: 20px;
      text-align: center;
    }
    .el-button {
      width: 100%;
    }
  }
}
</style>
