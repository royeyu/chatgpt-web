<script lang="ts" setup>
import { NCard, NGrid, NGridItem } from 'naive-ui'
import { useRouter } from 'vue-router'
import './home.less'

const router = useRouter()

const modules = [
  {
    name: 'ChatGPT3.5',
    description: 'ChatGPT3.5使用了更大的模型容量、更高的生成准确性和一致性以及更快的训练速度。',
    route: '/chat',
  },
  {
    name: 'ChatGLM',
    description: '开源的、支持中英双语的对话语言模型，基于 General Lananage Model (GLM) 架构。',
    route: 'http://zsy0601.xyz:3000/',
  },
]

function goToModule(route: string) {
// 如果路由route不是以'http'或'https'开头，则使用Vue Router的replace()方法进行路由跳转
  if (!/^http(s)?:\/\//.test(route)) {
    const resolvedRoute = router.resolve(route.replace('/home', '/chat')).href
    window.open(resolvedRoute, '_blank')
  }
  else {
  // 否则，使用window.open()方法打开URL
    window.open(route, '_blank')
  }
}
</script>

<template>
  <div class="flex h-full dark:bg-neutral-800">
    <div class="px-4 m-auto max-w-5xl">
      <h2 class="text-3xl font-bold text-center text-slate-800 dark:text-neutral-200 mb-8">
        选择使用的大模型
      </h2>
      <NGrid :cols="3" :rows="Math.ceil(modules.length / 3)">
        <NGridItem v-for="(module, index) in modules" :key="index">
          <NCard class="cursor-pointer module-card" @click="goToModule(module.route)">
            <div>
              <h3 class="module-title">
                {{ module.name }}
              </h3>
              <p class="module-description">
                {{ module.description }}
              </p>
            </div>
          </NCard>
        </NGridItem>
      </NGrid>
    </div>
  </div>
</template>
