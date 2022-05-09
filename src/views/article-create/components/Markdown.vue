<template>
  <div class="markdown-container">
    <!-- 渲染区 -->
    <div id="markdown-box"></div>
    <div class="bottom">
      <el-button type="primary" @click="onSubmitClick">{{ $t('msg.article.commit') }}</el-button>
    </div>
  </div>
</template>

<script setup>
import { commitArticle } from './commit'
const props = defineProps({
  title: {
    required: true,
    type: String
  }
})

const emits = defineEmits(['onSuccess'])
// 处理提交
const onSubmitClick = async () => {
  // 创建文章
  const res = await commitArticle({
    title: props.title,
    content: mkEditor.getHTML()
  })
  alert(JSON.stringify(res))
  await commitArticle({
    title: props.title,
    content: mkEditor.getHTML()
  })

  mkEditor.reset()
  emits('onSuccess')
}
</script>

<style lang="scss" scoped>
.markdown-container {
  .bottom {
    margin-top: 20px;
    text-align: right;
  }
}
</style>
