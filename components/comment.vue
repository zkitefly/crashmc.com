<template>
  <div class="comments">
    <component
      v-if="showComment"
      src="https://giscus.app/client.js"
      :is="'script'"
      :key="title"
      :data-repo="giscusConfig.repo"
      :data-repo-id="giscusConfig.repoId"
      :data-category="giscusConfig.category"
      :data-category-id="giscusConfig.categoryId"
      :data-mapping="giscusConfig.mapping"
      :data-strict="giscusConfig.strict"
      :data-reactions-enabled="giscusConfig.reactionsEnabled"
      :data-emit-metadata="giscusConfig.emitMetadata"
      :data-input-position="giscusConfig.inputPosition"
      :data-lang="giscusConfig.lang"
      :data-theme="giscusConfig.theme"
      :data-loading="giscusConfig.loading" />
  </div>
</template>
<script lang="ts" setup>
  import { useData, useRoute } from "vitepress"
  import { reactive, ref, watch } from "vue"

  const route = useRoute()

  const { title } = useData()

  // params generate in https://giscus.app/zh-CN
  const giscusConfig = reactive({
    repo: "GlobeMC/crashmc.com",
    repoId: "R_kgDOKBR8xw",
    category: "Giscus",
    categoryId: "DIC_kwDOKBR8x84CYOmB",
    mapping: "title",
    strict: "0",
    reactionsEnabled: "1",
    emitMetadata: "0",
    inputPosition: "top",
    theme: "preferred_color_scheme",
    lang: "zh-CN",
    loading: "lazy",
  })

  const showComment = ref(true)
  watch(
    () => route.path,
    () => {
      showComment.value = false
      setTimeout(() => {
        showComment.value = true
      }, 200)
    },
    {
      immediate: true,
    },
  )
</script>
<style>
  /* // TODO 使用giscus自定义主题结合vitepress主题切换 */
  .comments {
    margin-top: 20px;
    padding: 20px;
    border-radius: 10px;
  }
</style>
