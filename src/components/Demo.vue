<template>
  <div class="demo">
    <h2>{{ component.__sourceCodeTitle }}</h2>
    <div class="demo-component">
      <component :is="component" />
    </div>
    <div class="demo-actions">
      <Button @click="toggleCode">查看代码</Button>
    </div>
    <div class="demo-code" v-if="codeVisible">
      <pre class="language-css" v-html="html" />
    </div>
  </div>
</template>

<script lang="ts">
import { computed, ref } from "vue";
import Button from "../lib/Button.vue";
import "prismjs";
// import "prismjs/themes/prism.css";
import "prismjs/themes/prism-okaidia.css";

const Prism = (window as any).Prism;

export default {
  components: {
    Button,
  },
  props: {
    component: Object,
  },
  setup(props) {
    const html = computed(() => {
      return Prism.highlight(props.component.__sourceCode, Prism.languages.html, "html");
    });
    const codeVisible = ref(false);
    const toggleCode = () => {
      codeVisible.value = !codeVisible.value;
    };

    return { Prism, html, codeVisible, toggleCode };
  },
};
</script>

<style lang="scss" scoped>
.demo {
  margin: 16px 0 32px;
  border: 1px solid var(--border-color);

  > h2 {
    padding: 8px 16px;
    font-size: 20px;
    border-bottom: 1px solid var(--border-color);
  }

  &-component {
    padding: 16px;
  }

  &-actions {
    padding: 8px 16px;
    border-top: 1px dashed var(--border-color);
  }

  &-code {
    padding: 8px 16px;
    border-top: 1px dashed var(--border-color);

    > pre {
      margin: 0;
      line-height: 1.1;
      font-family: Consolas, "Courier New", Courier, monospace;
    }
  }
}
</style>
