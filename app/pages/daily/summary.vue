<template>
  <el-space direction="vertical" class="w-full" fill>
    <div >
      <el-button type="primary" class="float-right">发送</el-button>
      <el-date-picker
        v-model="dateRange"
        type="datetimerange"
        :shortcuts="shortcuts"
        range-separator="~"
        start-placeholder="Start date time"
        end-placeholder="End date time"
        class="float-left"
      />
    </div>
    <el-input
      v-model="content"
      class="min-w-2/3"
      :rows="20"
      type="textarea"
      placeholder="Please input"
    />
  </el-space>
</template>

<script setup lang="ts">
const dateRange = ref([new Date(),new Date()]);
const content = ref();
const defaultDateTime = new Date(new Date().setHours(17, 45, 0, 0));
const shortcuts = [
  {
    text: "18:45",
    value: () => {
      return [defaultDateTime, new Date(new Date().setHours(18, 45, 0, 0))];
    },
  },
  {
    text: "19:15",
    value: () => {
      return [defaultDateTime, new Date(new Date().setHours(19, 15, 0, 0))];
    },
  },
  {
    text: "19:45",
    value: () => {
      return [defaultDateTime, new Date(new Date().setHours(19, 45, 0, 0))];
    },
  },
  {
    text: "20:15",
    value: () => {
      return [defaultDateTime, new Date(new Date().setHours(20, 15, 0, 0))];
    },
  },
  {
    text: "20:45",
    value: () => {
      return [defaultDateTime, new Date(new Date().setHours(20, 45, 0, 0))];
    },
  },
  {
    text: "21:15",
    value: () => {
      return [defaultDateTime, new Date(new Date().setHours(21, 15, 0, 0))];
    },
  },
];
function initData() {
  dateRange.value = [
    defaultDateTime,
    new Date(new Date().setHours(18, 45, 0, 0)),
  ];
  content.value = "1.\n2.\n[勤奋时间][17:45][18:45]\n";
}
// TODO 修改勤奋时间
watch(dateRange,(newDateRange: any[],oldDateRange: any[])=>{
    if(newDateRange[1]?.getTime()!==oldDateRange[1]?.getTime()){
        const regx = /(?<=\[勤奋时间\]\[17:45\]\[)(?<endDate>.*?)(?=\])/gi
        const hours = newDateRange[1].getHours()
        const minute = newDateRange[1].getMinutes()
        content.value = (content.value||'').replace(regx,`${hours}:${minute}`)
    }
})
onMounted(() => {
  initData();
});
</script>

<style scoped lang="scss"></style>
