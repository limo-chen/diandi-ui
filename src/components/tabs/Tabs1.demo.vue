<demo>
  默认样式
</demo>

<template>
  <div>
    <Tabs v-model:selected="x">
      <Tab title="导航1">内容 1</Tab>
      <Tab title="导航2">内容 2</Tab>
    </Tabs>
  </div>
</template>

<script lang="ts">
import Tabs from "../../lib/Tabs.vue";
import Tab from "../../lib/Tab.vue";
import { ref } from "vue";

export default {
  components: { Tabs, Tab },
  setup() {
    const x = ref("导航1");
    return { x };
  },
};
</script>
