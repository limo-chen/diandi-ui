<template>
  <button @click="toggle" class="water-switch" :class="{ checked: value }">
    <span></span>
  </button>
</template>

<script lang="ts">
export default {
  props: {
    value: Boolean,
  },
  setup(props, context) {
    const toggle = () => {
      context.emit("update:value", !props.value);
    };
    return { toggle };
  },
};
</script>

<style lang="scss" scoped>
.water-switch {
  position: relative;
  width: var(--switch-box-width);
  height: var(--switch-box-height);
  border: none;
  border-radius: var(--switch-box-radius);
  background: var(--switch-bg-color);

  > span {
    position: absolute;
    top: 2px;
    left: 2px;
    width: var(--switch-circle-width);
    height: var(--switch-circle-height);
    border-radius: var(--switch-circle-radius);
    background: var(--bg-color-white);
    transition: all 250ms;
  }

  &.checked {
    background: var(--switch-checked-color);

    > span {
      left: calc(100% - 18px - 2px);
    }
  }

  &.checked:active {
    > span {
      width: 18px + 4px;
      margin-left: -4px;
    }
  }

  &:focus {
    outline: none;
  }

  &:active {
    > span {
      width: 18px + 4px;
    }
  }
}
</style>
