<script setup lang="ts">
import { FileUpload, ImageUpload } from '#/components/upload';
import { JsonPreview, Page } from '@vben/common-ui';
import { Alert, RadioGroup } from 'ant-design-vue';
import { ref } from 'vue';

const resultField = ref<'ossId' | 'url'>('ossId');

const imageList = ref([]);
const fileList = ref(['111', '2222']);
const fieldOptions = [
  { label: 'ossId', value: 'ossId' },
  { label: '链接地址', value: 'url' },
];
const fileAccept = ['xlsx', 'word', 'pdf'];

const signleImage = ref<string>('1745443704356782081');
</script>

<template>
  <Page content-class="flex flex-col gap-[12px]">
    <div class="bg-background flex flex-col gap-[12px] rounded-lg p-6">
      <Alert
        :show-icon="true"
        message="新特性: 设置max-number为1时, 会被绑定为string而非string[]类型 省去手动转换"
      />
      <ImageUpload
        v-model:value="signleImage"
        :max-number="1"
        result-field="ossId"
      />
      <JsonPreview :data="signleImage" />
    </div>
    <div class="bg-background flex flex-col gap-[12px] rounded-lg p-6">
      <div class="flex gap-[8px]">
        <span>返回字段: </span>
        <RadioGroup v-model:value="resultField" :options="fieldOptions" />
      </div>
      <ImageUpload
        v-model:value="imageList"
        :max-number="3"
        :result-field="resultField"
      />
      <JsonPreview :data="imageList" />
    </div>
    <div class="bg-background flex flex-col gap-[12px] rounded-lg p-6">
      <div class="flex gap-[8px]">
        <span>返回字段: </span>
        <RadioGroup v-model:value="resultField" :options="fieldOptions" />
      </div>
      <Alert
        :message="`支持的文件类型：${fileAccept.join(', ')}`"
        :show-icon="true"
        type="info"
      />
      <FileUpload
        v-model:value="fileList"
        :accept="fileAccept"
        :max-number="3"
        :result-field="resultField"
      />
      <JsonPreview :data="fileList" />
    </div>
  </Page>
</template>
