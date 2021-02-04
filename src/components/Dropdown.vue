<template>
  <div class="dropdown" :class="{open: value}">
    <slot name="text">
      <div @click="$emit('input', !value)">
        <i class="arrow-down"></i>
      </div>
    </slot>

    <div class="dropdown-list">
      <slot name="list"></slot>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Dropdown',

    props: {
      value: {
        type: Boolean,
        default: false
      },
    },
  }
</script>

<style lang="scss" scoped>
.dropdown {
  position: relative;
  &.open .dropdown-list {
    display: block;
  }
}

.dropdown-list {
  position: absolute;
  z-index: 2;
  top: 100%;
  left: 0;
  min-width: 170px;
  display: none;
  box-shadow: 1px 1px 18px #ccc;

  button {
    width: 100%;
    text-align: left;
    cursor: pointer;
    &:hover {
      background: #f3f3f3;
    }
  }
}

.dropdown-item {
  padding: 15px 25px;
  background: #fff;
  color: #333;
}

.dropdown-item + .dropdown-item {
  border-top: 1px solid #ccc;
}
</style>