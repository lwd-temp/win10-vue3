<template>
  <div class="container">
    <div class="nav">
      <ul>
        <li
          v-for="(item, index) in items"
          :key="index"
          @click="selectItem(index)"
          :class="{ active: index === activeIndex }"
        >
          {{ item }}
        </li>
      </ul>
    </div>
    <div class="setting">
      <div v-if="0 === activeIndex">
        <div class="setting-item">
          <h1 class="setting-title">{{ i18n('screen') }}</h1>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { inject, ref } from 'vue';
import { i18n } from '@/packages/computer/i18n';
import { System } from '@packages/kernel';
const system = inject<System>('system')!;

const items = [i18n('screen')];

const activeIndex = ref(0);

const selectItem = (index: number) => {
  activeIndex.value = index;
};
</script>
<style scoped>
@import './setStyle.css';
.ctrl {
  width: 100px;
}
.setting-item {
  display: flex;
  align-items: center;
}
</style>
