<template>
  <span class="separator__wrapper">
    <div class="separator"></div>
  </span>
  <!-- <span
        class="separator__wrapper"
        style="width: 1px; height: 52px; background-color: white"
      >
        <div
          class="separator"
          style="
            width: 100%;
            height: 28px;
            background-color: #afafb0;
            margin: 12px 0;
          "
        ></div>
      </span> -->
</template>

<script></script>

<style scoped>
.separator {
  width: 100%;
  height: 28px !important;
  background-color: #afafb0;
  margin: 12px 0;
}

.separator__wrapper {
  width: 1px !important;
  max-width: 1px !important;
  min-width: 1px !important;
  height: 52px;
  background-color: transparent !important;
}

@media (max-width: 794px) {
  .separator__wrapper {
    height: 32px !important;
  }

  .separator {
    margin: 2px 0;
  }
}
</style>
