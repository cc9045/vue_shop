<template>
  <div class="login_container">
    <div class="login_box">
      <div class="avatar_box">
        <img src="../assets/avatar.png" alt="">
      </div>
      <!-- 登录表单区 -->
      <el-form label-width="60px" class="login_form">
        <el-form-item label="用户名">
          <el-input
          prefix-icon="iconfont icon-user"></el-input>
        </el-form-item>
        <el-form-item label="密码">
          <el-input
          prefix-icon="iconfont icon-3702mima"></el-input>
        </el-form-item>
        <el-form-item class="btns">
          <el-button type="primary">登录</el-button>
          <el-button type="primary" plain>注册</el-button>
        </el-form-item>
       </el-form>
    </div>
  </div>
</template>

<script>
export default {

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