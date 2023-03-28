<template>
  <template v-if="visible">
    <Teleport to="body">
      <div class="water-dialog-overlay" @click="onClickOverlay"></div>
      <div class="water-dialog-wrapper">
        <div class="water-dialog">
          <header>
            <slot name="title" />
            <span @click="close" class="water-dialog-close"></span>
          </header>
          <main>
            <slot name="content" />
          </main>
          <footer>
            <Button level="main" @click="ok">OK</Button>
            <Button @click="cancel">Cancel</Button>
          </footer>
        </div>
      </div>
    </Teleport>
  </template>
</template>

<script lang="ts">
import Button from "./Button.vue";

export default {
  props: {
    visible: {
      type: Boolean,
      default: false,
    },
    closeOnClickOverlay: {
      type: Boolean,
      default: true,
    },
    ok: {
      type: Function,
    },
    cancel: {
      type: Function,
    },
  },
  components: { Button },
  setup(props, context) {
    const close = () => {
      context.emit("update:visible", false);
    };
    const onClickOverlay = () => {
      if (props.closeOnClickOverlay) {
        close();
      }
    };
    const ok = () => {
      // 新语法：props.ok?.() !== false
      if (props.ok && props.ok() !== false) {
        close();
      }
    };
    const cancel = () => {
      // 新语法：props.cancel?.()
      props.cancel && props.cancel();
      close();
    };
    return { close, onClickOverlay, ok, cancel };
  },
};
</script>

<style lang="scss" scoped>
.water-dialog {
  min-width: 15em;
  max-width: 90%;
  border-radius: var(--button-radius);
  background: var(--bg-color-white);
  box-shadow: 0 0 3px fade_out(#000, 0.5);

  &-overlay {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background: fade_out(#000, 0.5);
    z-index: 10;
  }

  &-wrapper {
    position: fixed;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    z-index: 11;
  }

  > header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 12px 16px;
    font-size: 20px;
    border-bottom: 1px solid var(--border-color);
  }

  > main {
    padding: 12px 16px;
  }

  > footer {
    text-align: right;
    padding: 12px 16px;
    border-top: 1px solid var(--border-color);
  }

  &-close {
    position: relative;
    display: inline-block;
    width: 16px;
    height: 16px;
    cursor: pointer;

    &::before,
    &::after {
      position: absolute;
      left: 50%;
      top: 50%;
      content: "";
      width: 100%;
      height: 1px;
      background: #000;
    }

    &::before {
      transform: translate(-50%, -50%) rotate(-45deg);
    }

    &::after {
      transform: translate(-50%, -50%) rotate(45deg);
    }
  }
}
</style>
