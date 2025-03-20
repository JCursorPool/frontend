<script setup lang="ts">
import { ref } from 'vue';

import { MarkdownPreviewer, Page } from '@vben/common-ui';

import { Skeleton } from 'ant-design-vue';

import changelog from '../../../../../../CHANGELOG.md?raw';

const content = ref(changelog);

const loading = ref(true);
</script>

<template>
  <Page :auto-content-height="true">
    <Skeleton v-show="loading" active />
    <MarkdownPreviewer
      v-model:value="content"
      height="100%"
      @mounted="loading = false"
    />
  </Page>
</template>
