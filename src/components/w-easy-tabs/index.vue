<script lang="ts" setup>
import type { ITabChangeValue } from './type'
import useAntTheme from '@/hooks/useAntTheme'
import type { IPublicOption } from '@/types'

const props = defineProps<IProps>()
const emit = defineEmits(['change'])

const { colorPrimary } = useAntTheme().fetchToken()

interface IProps {
  tabs: IPublicOption[]
}

const currentIndex = ref(0)
// 切换激活
function changeActive(index: number) {
  currentIndex.value = index
  const info: ITabChangeValue = { index, value: props.tabs[index] }
  emit('change', info)
}
</script>

<template>
  <div class="w-easy-tabs flex">
    <div
      v-for="(item, index) in tabs" :key="index"
      class="tab flex justify-center items-center"
      :class="{ tabActive: currentIndex === index }"
      @click="changeActive(index)"
    >
      {{ item.label }}
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .tab {
    padding: 5px 10px;
    border: 1px solid #ccc;
    line-height: 20px;
    font-size: 13px;
    cursor: pointer;
    transition: 0.4s all linear;
  }
  .tabActive {
    color: v-bind(colorPrimary);
    border-color: v-bind(colorPrimary);
  }
</style>
