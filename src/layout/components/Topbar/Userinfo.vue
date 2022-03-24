<template>
  <el-dropdown trigger="click">
    <div class="userinfo">
      <el-avatar
        size="small"
        src="https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png"
      ></el-avatar>
      <span style="margin-left: 8px;">
        {{ userinfo.name }}
      </span>
    </div>
    <template #dropdown>
      <el-dropdown-menu>
        <lock-modal />
        <el-dropdown-item @click="logout">退出登录</el-dropdown-item>
      </el-dropdown-menu>
    </template>
  </el-dropdown>
</template>
<script>
import { defineComponent } from 'vue'
import { useStore } from 'vuex'
import { useRouter } from 'vue-router'
import { useUserinfo } from '@/components/Avatar/hooks/useUserinfo'
import LockModal from './LockModal.vue'
import { UserFilled } from '@element-plus/icons'
export default defineComponent({
  components: {
    LockModal,
    UserFilled,
  },
  setup() {
    const store = useStore()
    const router = useRouter()
    const { userinfo } = useUserinfo()
    // 退出
    const logout = () => {
      // 清除token
      store.dispatch('app/clearToken')
      router.push('/login')
    }
    return {
      userinfo,
      logout,
      UserFilled,
    }
  },
})
</script>

<style lang="scss" scoped>
.userinfo {
  padding: 0 16px;
  line-height: 48px;
  cursor: pointer;
  display: flex;
  align-items: center;
  &:hover {
    background: #f5f5f5;
  }
  .el-icon-user {
    font-size: 20px;
    margin-right: 8px;
  }
  .avatar {
    margin-right: 8px;
    width: 32px;
    height: 32px;
    border-radius: 50%;
  }
}
</style>
