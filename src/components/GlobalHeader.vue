<template>
  <div id="globalHeader">
    <div class="left-bar">
      <RouterLink to="/">
        <div class="title-bar">
          <img class="logo" src="../assets/logo.png" alt="logo" />
          <div class="title">PixelARK</div>
        </div>
      </RouterLink>
      <a-menu v-model:selectedKeys="current" mode="horizontal" :items="items" @click="doMenuClick" />
    </div>

    <div class="user-login-status">
      <div v-if="loginUserStore.loginUser.id">
        {{ loginUserStore.loginUser.userName ?? '无名' }}
      </div>
      <div v-else>
        <a-button type="primary" href="/user/login">登录</a-button>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { h, ref } from 'vue';
import { HomeOutlined } from '@ant-design/icons-vue';
import type { MenuProps } from 'ant-design-vue';
import { useRouter } from "vue-router";
import { useLoginUserStore } from "@/stores/user";

const router = useRouter();
const loginUserStore = useLoginUserStore();

// 当前选中菜单
const current = ref<string[]>([]);
// 监听路由变化，更新当前选中菜单
router.afterEach((to, from, next) => {
  current.value = [to.path];
});
const items = ref<MenuProps['items']>([
  {
    key: '/',
    icon: () => h(HomeOutlined),
    label: '主页',
    title: '主页',
  },
  {
    key: '/about',
    label: '关于',
    title: '关于',
  },
]);
// 路由跳转事件
const doMenuClick = ({ key }: { key: string }) => {
  router.push({
    path: key,
  });
};

</script>

<style scoped>
#globalHeader {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.left-bar {
  display: flex;
  align-items: center;
}

.title-bar {
  display: flex;
  align-items: center;
  margin-right: 24px;
}

.title {
  color: black;
  font-size: 18px;
  margin-left: 16px;
}

.logo {
  height: 48px;
}
</style>
