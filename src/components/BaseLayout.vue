<template>
    <div class="h-full">
      <el-container class="h-full">
        <el-header></el-header>
        <el-container class="bg-gray-200 container w-full">
          <el-aside width="200px" class="border-r border-gray-300"></el-aside>
          <el-main class="overflow-hidden">
            <div class="inner-container overflow-hidden">
              <ListContainer />
            </div>
          </el-main>
        </el-container>
      </el-container>
    </div>
</template>
<script setup> 
import ListContainer from './ListContainer.vue'
</script>
<style lang="scss" scoped>
.container {
  height: calc(100vh - 60px);
}
.inner-container {
  height: calc(100vh - 60px - 40px);
}
</style>