<template>
  <div class="menu-style">
    <!-- <div class="collapse-style">
      <el-icon :size="20" v-if="isCollapse" @click="handleClose"><Expand /></el-icon>
      <el-icon :size="20" v-else @click="handleClose"><Fold /></el-icon>
    </div> -->
    <el-menu default-active="1" class="el-menu-vertical-demo" :collapse="isCollapse">
      <div v-for="(item, index) in menu" :key="index">
        <el-sub-menu
          v-if="item.children && item.children.length"
          :index="item.index"
        >
          <template #title>
            <el-icon :size="20">
              <component :is="item.icon" />
            </el-icon>
            <span>{{ item.title }}</span>
          </template>
          <el-menu-item
            v-for="(subItem, index) in item.children"
            :key="index"
            :index="subItem.index"
            @click="handleMenu(subItem)"
          >
            <el-icon :size="20">
              <component :is="subItem.icon" />
            </el-icon>
            <span>{{ subItem.title }}</span>
          </el-menu-item>
        </el-sub-menu>

        <el-menu-item v-else :index="item.index" @click="handleMenu(item)">
          <el-icon :size="20">
            <component :is="item.icon" />
          </el-icon>
          <span>{{ item.title }}</span>
        </el-menu-item>
      </div>
    </el-menu>
  </div>
</template>
  
<script setup>
import { ref } from 'vue'
import { useRoute, useRouter } from "vue-router";
import { menu } from "@/mock/menu.ts";
const router = useRouter();
const isCollapse = ref(false)
const handleOpen = (key, keyPath) => {
  console.log(key, keyPath);
};
const handleClose = () => {
  isCollapse.value=!isCollapse.value
};
const handleMenu = (item) => {
  if (item.path) {
    router.push({ path: item.path });
  } 
};
</script>
<style scope lang="scss">
.menu-style {
  position: relative;
  .collapse-style {
    z-index: 2;
    position: absolute;
    top: 0;
    right: 0;
  }
}
</style>
<style>
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 200px;
  min-height: 400px;
}
</style>