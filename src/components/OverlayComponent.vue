<template>
  <div
    wire:loading
    :class="opacity + loaderBackground"
    class="absolute top-0 left-0 right-0 bottom-0 w-full z-50 overflow-hidden flex flex-col items-center justify-center min-h-65"
  >
    <div
      :class="
        rounded + borderFrontColor + borderBackColor + borderWidth + loaderSize
      "
      class="loader ease-linear mb-4"
    ></div>
  </div>
</template>
<script>
export default {
  props: {
    rounded: {
      type: String,
      required: false,
      default: "rounded-full",
    },
    opacity: {
      type: String,
      required: false,
      default: "opacity-75",
    },
    borderFrontColor: {
      type: String,
      required: false,
      default: " border-t-blue-700 dark:border-t-blue-700 ",
    },
    borderBackColor: {
      type: String,
      required: false,
      default: " border-gray-400 dark:border-gray-400 ",
    },
    borderWidth: {
      type: String,
      required: false,
      default: " border-4 ",
    },
    loaderSize: {
      type: String,
      required: false,
      default: " w-12 h-12 ",
    },
    loaderBackground: {
      type: String,
      required: false,
      default: " bg-gray-100 dark:bg-gray-900 ",
    },
  },
};
</script>
<style lang="scss">
@import "/src/styles/components/_overlay.scss";
</style>
