<template>
  <a-row type="flex" align="start">
    <a-col :md="16" :xs="24">
      <a-card title="历史记录" v-if="hasHistory">
        <a-list item-layout="horizontal" :data-source="['']">
          <template #renderItem="">
            <a-list-item>
              <a-list-item-meta title="历史记录" />
              <template #actions>
                <a-button disabled>编辑</a-button>
                <a-button danger @click="clearHistory()">清除</a-button>
              </template>
            </a-list-item>
          </template>
        </a-list>
      </a-card>
      <a-card title="本地保存">
        <a-list item-layout="horizontal" :data-source="['']">
          <template #renderItem="">
            <a-list-item>
              <a-list-item-meta title="" />
              <template #actions>
                <a-button @click="clearHistory()">编辑</a-button>
                <a-button danger @click="clearHistory()">清除</a-button>
              </template>
            </a-list-item>
          </template>
        </a-list>
      </a-card>
    </a-col>
    <a-col :md="12" :xs="24" style="margin-left: 16px">
    </a-col>
  </a-row>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { message } from 'ant-design-vue'
import { globalStore } from '../core/globalStore.ts'

const store = globalStore();

//是否存在历史记录
const hasHistory = computed(() => {
  if (!store.history.data || store.history.data.length == 0){
    return false;
  }
  return true;
})

//清除历史记录
const clearHistory = () => {
  store.history.data = null
  message.success("清除成功！")
}

</script>

<style scoped></style>
