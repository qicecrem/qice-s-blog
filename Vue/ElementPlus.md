# 引入依赖
```
pnpm install element-plus
```
# 按需引入
借助unplugin-vue-components和unplugin-auto-import插件实现按需引入。
首先，安装插件：
```
pnpm install -D unplugin-vue-components unplugin-auto-import
```
接着，在vite.config.js（若使用 Vite）或者webpack.config.js（若使用 Webpack）里进行配置。以 Vite 为例：
```
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

export default defineConfig({
  plugins: [
    vue(),
    AutoImport({
      resolvers: [ElementPlusResolver()],
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    }),
  ],
})
```
# 全局引入
在main.js（Vue 3 项目）或者main.ts（Vue 3 + TypeScript 项目）中进行全局引入
```
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'

const app = createApp(App)
app.use(ElementPlus)
app.mount('#app')
```
# Icon 图标
安装
```
pnpm install @element-plus/icons-vue
```
# 全局引入图标
在项目的入口文件（如 main.js 或 main.ts）中进行全局引入：
```
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import * as ElementPlusIconsVue from '@element-plus/icons-vue'
import App from './App.vue'

const app = createApp(App)
app.use(ElementPlus)

// 全局注册图标
for (const [key, component] of Object.entries(ElementPlusIconsVue)) {
  app.component(key, component)
}

app.mount('#app')
```
在 Vue 组件中可以直接使用注册好的图标：
# 按需引入
在需要使用图标的组件中，按需引入所需的图标：
```
<template>
  <div>
    <!-- 使用搜索图标 -->
    <el-icon><Search /></el-icon>
  </div>
</template>

<script setup>
import { Search } from '@element-plus/icons-vue'
</script>
```
