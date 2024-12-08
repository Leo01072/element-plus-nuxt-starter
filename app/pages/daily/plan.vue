<template>
  <el-space direction="vertical" class="w-full" fill>
    <div>
      <el-button type="primary" class="float-right">发送</el-button>
      <el-date-picker
        v-model="datetime"
        type="date"
        placeholder="Pick a day"
        class="float-left"
      />
    </div>
    <el-input
      v-model="content"
      class="w-2/3 min-w-[500px]"
      :rows="20"
      type="textarea"
      placeholder="Please input"
    />
  </el-space>
</template>

<script setup lang="ts">
const datetime = ref();
const content = ref();
function initData() {
  datetime.value = new Date();
  content.value = "1.";
}
onMounted(() => {
  initData();
});
</script>

<style scoped lang="scss"></style>
