<template>
  <div class="main">
    <el-container class="main-content">
      <el-aside :width="isCollapse ? collapseWidth : '210px'" class="main-menu">
        <nav-menu :collapse="isCollapse" />
      </el-aside>
      <el-container class="page">
        <el-header class="page-header">
          <nav-header @foldChange="handleFoldChange" />
        </el-header>
        <el-main class="page-content">
          <div class="page-info">
            <router-view></router-view>
          </div>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

import navMenu from '@/components/nav-menu'
import navHeader from '@/components/nav-header'

import { reactiveWidth } from '@/utils/reactive-width'

const isCollapse = ref(false)
const collapseWidth = reactiveWidth('0', '64px')

const handleFoldChange = (isFold: boolean) => {
  isCollapse.value = isFold
}
</script>

<style scoped lang="less">
@media (max-width: 768px) {
  .main-menu {
    position: fixed;
    top: 50px;
    left: 0;
    height: calc(100% - 48px); /* 移动端需减去导航头高度 */
    z-index: 999;
  }
}

.main {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.main-content,
.page {
  height: 100%;
}

.page-content {
  height: calc(100% - 48px);

  .page-info {
    border-radius: 5px;
    background-color: #fff;
  }
}

.el-header,
.el-footer {
  display: flex;
  color: #333;
  align-items: center;
}

.el-header {
  height: 48px !important;
}

.el-aside {
  overflow-x: hidden;
  overflow-y: auto;
  line-height: 200px;
  text-align: left;
  cursor: pointer;
  background-color: #001529;
  transition: width 0.3s linear;
  scrollbar-width: none; /* firefox */
  -ms-overflow-style: none; /* IE 10+ */

  &::-webkit-scrollbar {
    display: none;
  }
}

.el-main {
  color: #333;
  text-align: center;
  background-color: #f0f2f5;
}
</style>
