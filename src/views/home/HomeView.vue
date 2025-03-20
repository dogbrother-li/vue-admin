<script setup lang="ts">
import MenuLeftView from '../../layout/MenuView.vue'
import MenuHeadView from '@/layout/MenuHeadView.vue'
</script>

<template>
  <div class="common-layout">
    <el-container>
      <el-header><MenuHeadView /></el-header>
      <el-container>
        <el-aside width="200px"><MenuLeftView /></el-aside>
        <el-main> This is home page </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<style scoped>
@media (min-width: 1024px) {
  .common-layout {
    height: 100%;
    box-sizing: border-box;
    overflow: hidden;
    background-color: #eff0f4;
  }
}
</style>
