<template>
  <button class="water-button" :class="classes" :disabled="disabled">
    <span v-if="loading" class="water-loadingIndicator"></span>
    <slot />
  </button>
</template>

<script lang="ts">
import { computed } from "vue";

export default {
  props: {
    theme: {
      type: String,
      default: "button",
    },
    size: {
      type: String,
      default: "normal",
    },
    level: {
      type: String,
      default: "normal",
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    loading: {
      type: Boolean,
      default: false,
    },
  },
  setup(props) {
    const { theme, size, level } = props;
    const classes = computed(() => {
      return [`water-theme-${theme}`, `water-size-${size}`, `water-level-${level}`];
    });
    return { classes };
  },
};
</script>

<style lang="scss" scoped>
.water-button {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  white-space: nowrap;
  height: var(--button-height);
  padding: 0 12px;
  border: 1px solid var(--border-color);
  border-radius: var(--button-radius);
  color: var(--text-color-black);
  background: var(--bg-color-white);
  box-shadow: 0 1px 0 fade-out(#000, 0.95);
  cursor: pointer;
  transition: background-color 250ms;

  & + & {
    margin-left: 8px;
  }

  &:hover,
  &:focus {
    color: var(--theme-color-blue-1);
    border-color: var(--theme-color-blue-1);
  }

  &:focus {
    outline: none;
  }

  &::-moz-focus-inner {
    border: 0;
  }

  &.water-theme-link {
    color: var(--theme-color-blue-1);
    border-color: transparent;
    box-shadow: none;

    &:hover,
    &:focus {
      color: lighten(#0081f9, 10%);
    }
  }

  &.water-theme-text {
    color: inherit;
    border-color: transparent;
    box-shadow: none;
    &:hover,
    &:focus {
      background: darken(#fff, 5%);
    }
  }

  &.water-size-big {
    height: 48px;
    padding: 0 16px;
    font-size: 24px;
  }

  &.water-size-small {
    height: 20px;
    padding: 0 4px;
    font-size: 12px;
  }

  &.water-theme-button {
    &.water-level-main {
      color: var(--text-color-white);
      background: var(--theme-color-blue-1);
      border-color: var(--theme-color-blue-1);

      &:hover,
      &:focus {
        background: darken(#0081f9, 10%);
        border-color: darken(#0081f9, 10%);
      }
    }

    &.water-level-danger {
      color: var(--text-color-white);
      background: var(--theme-color-red);
      border-color: var(--theme-color-red);

      &:hover,
      &:focus {
        background: darken(#ff585d, 10%);
        border-color: darken(#ff585d, 10%);
      }
    }
  }

  &.water-theme-link {
    &.water-level-danger {
      color: var(--theme-color-red);

      &:hover,
      &:focus {
        color: darken(#ff585d, 10%);
      }
    }
  }

  &.water-theme-text {
    &.water-level-main {
      color: var(--theme-color-blue-1);

      &:hover,
      &:focus {
        color: darken(#0081f9, 10%);
      }
    }

    &.water-level-danger {
      color: var(--theme-color-red);

      &:hover,
      &:focus {
        color: darken(#ff585d, 10%);
      }
    }
  }

  &.water-theme-button {
    &[disabled] {
      color: var(--text-color-muted);
      cursor: not-allowed;

      &:hover {
        border-color: var(--text-color-muted);
      }
    }
  }

  &.water-theme-link,
  &.water-theme-text {
    &[disabled] {
      color: var(--text-color-muted);
      cursor: not-allowed;
    }
  }

  > .water-loadingIndicator {
    display: inline-block;
    width: 10px;
    height: 10px;
    margin-right: 4px;
    border-color: var(--theme-color-blue-1) var(--theme-color-blue-1) var(--theme-color-blue-1)
      transparent;
    border-style: solid;
    border-width: 2px;
    border-radius: 8px;
    animation: water-spin 1s infinite linear;
  }
}

@keyframes water-spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
