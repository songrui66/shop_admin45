<template>
  <div class="index">
    <el-container class="el-heade">
      <el-header>
        <img src="../assets/logo.png" alt />
        <h1>电商后台管理系统</h1>
        <div class="right">
          <span>欢迎光临~</span>
          <span>
            <a href="javascript:;" @click="getOut">退出</a>
          </span>
        </div>
      </el-header>
      <el-container>
        <!-- 侧边导航栏 -->
        <el-aside width="200px">
          <el-menu
            default-active="2"
            class="el-menu-vertical-demo"
            background-color="#545c64"
            text-color="#fff"
            active-text-color="#ffd04b"
          >
            <el-submenu index="1">
              <template slot="title">
                <i class="el-icon-location"></i>
                <span>导航一</span>
              </template>
                <el-menu-item index="1-1">
                  <i class="el-icon-menu"></i>
                  <span slot="title">导航二</span>
                </el-menu-item>
            </el-submenu>
          </el-menu>
        </el-aside>
        <!-- 主体部分 -->
        <el-main></el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
export default {
  data () {
    return {

    }
  },
  methods: {
    getOut () {
      this.$confirm('你确定退出该系统吗?', '温馨提示', { type: 'warning ' }).then(() => {
        this.$message.success('删除成功')
        localStorage.removeItem('token')
        this.$router.push('/login')
      }).catch(() => {
        this.$message.error('取消删除')
      })
    }
  }
}
</script>

<style lang='scss' scoped>
.index {
  width: 100%;
  height: 100%;
  .el-heade {
    width: 100%;
    height: 100%;
    .el-header {
      background-color: #d8d8d8;
      display: flex;
      img {
        display: block;
        width: 147px;
        height: 40px;
        text-align: left;
        margin-top: 10px;
        margin-left: 20px;
      }
      h1 {
        text-align: center;
        line-height: 60px;
        height: 60px;
        flex: 1;
      }
      .right {
        text-align: right;
        line-height: 60px;
        height: 60px;
        font-weight: 600;
        :nth-child(2) {
         a{
            color: orange;
          }
        }
      }
    }
    .el-aside {
      background-color: #545c64;
      .el-menu{
        border-right: none;
      }
    }
  }
}
</style>
