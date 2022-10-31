<template>
  <div class="login_container">
    <div class="login_box">
      <div class="avatar_box">
        <img src="../assets/avatar.png" alt="">
      </div>
      <!-- 登录表单区 -->
      <el-form ref="loginFormRef" :model="loginForm" :rules="loginFormRules" label-width="60px" class="login_form"
      :hide-required-asterisk="true">
        <el-form-item label="用户名" prop="username"> <!-- prop对应rules规则约束，只能在item项中声明 -->
          <el-input v-model="loginForm.username"
          prefix-icon="iconfont icon-user"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="password">
          <el-input v-model="loginForm.password" show-password
          prefix-icon="iconfont icon-3702mima"></el-input>
        </el-form-item>
        <el-form-item class="btns">
          <el-button type="primary" @click="login">登录</el-button>
          <el-button type="info" @click="resetForm">重置</el-button>
        </el-form-item>
       </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      //登录表单数据绑定对象 
      loginForm: {
        username: 'admin',
        password: '123456'
      },
      //登录表单验证规则对象
      loginFormRules: {
        //验证用户名是否合法，类型为数组对象
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min:3, max: 10, message: '长度在3-10个字符', trigger: 'blur'}
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 15, message: '长度在6-15个字符', trigger: 'blur' },
          {
            //正则验证
            // pattern: /^(?!^\d+$)(?!^[a-zA-Z]+$)[0-9a-zA-Z]{4,23}$/,//必须包含数字和字母
            // message: '请输入正确的密码,密码必须包含数字和字符', trigger: 'blur'
            pattern: /^[A-Za-z0-9]+$/,//只由数字和字母组成，不能包含特殊字符
            message: '请输入正确的密码,不能包含特殊字符', trigger: 'blur'
          }
        ]
      }
    }
  },
  methods: {
    //重置按钮重置登录表单
    resetForm() {
      console.log(this);
      //清除表单，ref获取引用声明的组件对象,resetFields是自带的表单清除函数
      this.$refs.loginFormRef.resetFields();
    },
    login() {
      //表单预验证，valid是一个回调函数的形参布尔值，用于判断验证是否通过
      this.$refs.loginFormRef.validate(async valid => {
        //console.log(valid);
        if (!valid) return;
        // const res = await this.$http.post("login", this.loginForm);
        // console.log(res);
        //赋值解构,直接提取data的数据
        const { data: res } = await this.$http.post("login", this.loginForm);
        //console.log(res);
        if (res.meta.status !== 200) return this.$message.error('登录失败！')
        this.$message.success('登录成功！')
        // 1. 将登录成功之后的 token，保存到客户端的 sessionStorage 中
        //   1.1 项目中出了登录之外的其他API接口，必须在登录之后才能访问
        //   1.2 token 只应在当前网站打开期间生效，所以将 token 保存在 sessionStorage 中
        window.sessionStorage.setItem('token', res.data.token)//sessionStorge是当前会话窗口
        // 2. 通过编程式导航跳转到后台主页，路由地址是 /home
        this.$router.push('/home')
      });
    }
  }
}
</script>

<style lang="less" scoped>
//scoped局部作用域，防止全局冲突
  .login_container{
    background-color: #5c93a8;
    height: 100%;
  }
  .login_box{
    width: 450px;
    height: 300px;
    background-color: #fff;
    border-radius: 3px; //圆角边框
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);

    .avatar_box{
      height: 100px;
      width: 100px;
      border: 1px solid #eee;//添加边框
      border-radius: 50%;
      padding: 5px; //内间距 
      box-shadow: 0 0 10px rgb(14, 76, 117);//阴影扩散
      margin: -65px auto 0 auto;
      background-color: rgb(67, 99, 109);
      // position: absolute;
      // left: 50%;
      // top: -10%;
      // transform: translate(-50%, -50%);//左边偏移
      img{
        width: 100%;
        height: 100%;
        border-radius: 50%;
        background-color: #eee;
      }
    }
  }

  .login_form {
    position: absolute;
    //位于底部
    bottom: 0;
    //宽度占满
    width: 100%;
    //左右间距
    padding: 30px 40px;
    //你想要设置的边框和内边距的值是包含在 width 内的。
    //也就是说，如果你将一个元素的 width 设为 100px，
    //那么这 100px 会包含它的 border 和 padding，内容区的实际宽度是 width 减去 (border + padding) 的值。
    box-sizing: border-box;
  }
  .btns {
    //弹性布局,聚友
    display: flex;
    justify-content: flex-end;
  }
</style>