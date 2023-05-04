<template>
    <el-calendar ref="calendar" v-model="value">
      <template #header="{ date }">
        <span>📅日历</span>
        <span>{{ date }}</span>
        <el-button-group>
            <el-button size="small" type="primary" :icon="DArrowLeft" @click="selectDate('prev-year')">
                上一年
            </el-button>

          <el-button size="small" type="primary" :icon="ArrowLeft" @click="selectDate('prev-month')">
            上个月
          </el-button>
          <el-button size="small" type="primary" @click="selectDate('today')">今天</el-button>
          <el-button size="small" type="primary"  @click="selectDate('next-month')">
            下个月<el-icon class="el-icon--right"><ArrowRight /></el-icon>
          </el-button>
          <el-button size="small" type="primary" @click="selectDate('next-year')">
            下一年<el-icon class="el-icon--right"><DArrowRight /></el-icon>
          </el-button>
        </el-button-group>
      </template>
      <template #date-cell="{ data }">
        <div class="date-cell-template">
          <p :class="data.isSelected ? 'is-selected' : ''">
            {{ data.day.split('-').slice(1).join('-') }}
        </p>
        <div v-for="(item, index) in textContent(data.day)" :key="index" class="date-cell-template-div">
          <span :class="data.isSelected ? 'is-selected' : ''">{{ item.event }}</span>
          <span>{{ item.emoji }}</span>
        </div>
        </div>
      </template>
    </el-calendar>
  </template>
  
  <script lang="ts" setup>
  import { ref, reactive } from 'vue'
  import { DArrowLeft, ArrowLeft } from '@element-plus/icons-vue'
  import { calendarEvent } from "../mock/CalendarEvent.json"

  const calendar = ref()
  const value = ref(new Date("04/25/2022"))
  const selectDate = (val: string) => {
    calendar.value.selectDate(val)
  }

  interface CalendarDataList {
    day: string
    event: string
    emoji: string
  }
  const state = reactive({
    calendarEvent: [] as CalendarDataList[]
  });
  state.calendarEvent = calendarEvent
  const textContent = (date: any) => {
    //当前date是拿到上面日历组件当前的日期值 根据该值去筛选测试数据找到对应各个日期下对应的数据return出去
    console.log(date, 1111);
    return state.calendarEvent.filter((item) => {
      return date === item.day;
    });
  };
  </script>

<style lang="less" scoped>
.is-selected {
  color: #1989fa;
}

.date-cell-template {
  margin-top: -15px;
}

.date-cell-template-div {
  margin-top: -10px;
}
</style>
