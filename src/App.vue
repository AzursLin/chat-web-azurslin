<script setup lang="ts">
import { NConfigProvider } from "naive-ui";
import { NaiveProvider } from "@/components/common";
import { useTheme } from "@/hooks/useTheme";
import { useLanguage } from "@/hooks/useLanguage";
import { ElMenu, ElMenuItem, ElRow, ElCol } from "element-plus";
import homeIcon from "@/icons/home.vue";
import messageIcon from "@/icons/message.vue";
const { theme, themeOverrides } = useTheme();
const { language } = useLanguage();
import { useRouter, useRoute } from 'vue-router'

const router = useRouter()
const route = useRoute() // 获取当前路由信息

// 点击直接跳转，无需判断
const handleSelect = (index: string) => {
  router.push(index).catch(err => err) // 忽略重复导航错误
}
</script>

<template>
  <NConfigProvider
    class="h-full app-layout"
    :theme="theme"
    :theme-overrides="themeOverrides"
    :locale="language"
  >
    <NaiveProvider>
      <ElRow>
        <ElCol :span="1"></ElCol>
        <ElCol :span="23">
          <ElMenu
            :default-active="route.path"
            class="el-menu-demo"
            mode="horizontal"
            @select="handleSelect"
          >
            <ElMenuItem index="/home">
              <template #title>
                <homeIcon size="24"></homeIcon>
                <span>首页</span>
              </template>
            </ElMenuItem>
            <ElMenuItem index="/chat">
              <template #title>
                <messageIcon size="24"></messageIcon>
                <span>消息</span>
              </template>
            </ElMenuItem>
          </ElMenu>
        </ElCol>
      </ElRow>
      <RouterView />
    </NaiveProvider>
  </NConfigProvider>
</template>
<style scoped>
/* 根布局：垂直 Flex，撑满父容器 */
.app-layout {
  display: flex;
  flex-direction: column;
  height: 100%; /* 继承 #app 的 100vh 高度 */
}


/* 可选：若内容需要内部滚动，单独设置 */
/* .content-scroll {
  height: 100%;
  overflow-y: auto;
} */
</style>
