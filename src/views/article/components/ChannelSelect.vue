<script setup>
import { artGetChannelsService } from '../../../api/article'
import { ref } from 'vue'

defineProps({ modelValue: { type: [Number, String] }, width: { type: String } }) //接收父
const emit = defineEmits(['update:modelValue']) //发送父

const channelList = ref([])
const getChannelList = async () => {
  const res = await artGetChannelsService()
  channelList.value = res.data.data
}
getChannelList()
</script>

<template>
  <el-select
    :modelValue="modelValue"
    @update:modelValue="emit('update:modelValue', $event)"
    :style="{ width }"
  >
    <!-- label展示给用户看的   value收集起来提交给后台的 -->
    <el-option
      v-for="channel in channelList"
      :key="channel.id"
      :label="channel.cate_name"
      :value="channel.id"
    ></el-option>
  </el-select>
</template>
