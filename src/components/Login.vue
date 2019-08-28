<template>
  <div class="login">
  <!-- form 表单 -->
    <el-form  :model = 'form' ref="form" :rules = 'rules'  label-width='80px'>
      <img src="../assets/avatar.jpg" alt="">
      <el-form-item label="用户名" prop='username'>
        <el-input v-model="form.username" placeholder="请输入用户名"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop='password'>
        <el-input v-model="form.password" type='password' placeholder='请输入密码'></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type='primary' @click="login">登录</el-button>
        <el-button type='default' class="resBtn" @click="reset">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      form: {
        username: '',
        password: ''
      },
      rules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 12, message: '长度在 3 到 12 个字符', trigger: ['blur', 'change'] }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 3, max: 12, message: '长度在 3 到 12 个字符', trigger: ['blur', 'change'] }
        ]
      }
    }
  },
  methods: {
    async login () {
      try {
        await this.$refs.form.validate()
        const { data, meta } = await this.$axios.post('login', this.form)
        if (meta.status === 200) {
          this.$message.success(meta.msg)
          localStorage.setItem('token', data.token)
          // 跳入index页面
          this.$router.push('/index')
        } else {
          this.$message.error(meta.msg)
        }
      } catch (error) {
        console.log(error)
      }
    },
    reset () {
      this.$refs.form.resetFields()
    }

  }

}
</script>

<style lang='scss' scoped>
 .login{
    width: 100%;
    height: 100%;
    background-color: #2d434c;
    overflow: hidden;
 }
 .el-form{
    width: 400px;
    background-color: #fff;
    margin: 200px auto;
    padding: 75px 30px 75px 30px;
    border-radius: 20px;
    position: relative;
    img{
      position: absolute;
      top:-72px;
      left: 50%;
      transform: translateX(-50%);
      border-radius: 50%;
      border: 5px solid #fff;
    }
    .resBtn{
      margin-left: 70px;
    }
 }
</style>
