<template>
  <div id="tab-bar">
    <slot></slot>
  </div>
</template>

<script>
export default {};
</script>
<style >
#tab-bar {
  width: 100%;
  position: fixed;
  bottom: 0;
  left: 0;
  display: flex;
  background-color: #f6f6f6;
  box-shadow: 0 -3px 1px rgba(100, 100, 100, 0.1);
}
</style>

