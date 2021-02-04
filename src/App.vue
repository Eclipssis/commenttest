<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="scss">

// Common styles 
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 40px;
}

// icons
.user-icon {
  display: inline-block;
  width: 15px;
  height: 15px;
  background: url('assets/user-icon.png');
  background-size: 100%;
  margin-bottom: 2px;
}

.arrow-down {
  display: inline-block;
  width: 15px;
  height: 15px;
  background: url('assets/arrow-down.png');
  background-size: 100%;
  margin-left: 5px;
  cursor: pointer;
}

// Buttons

button {
  border: none;
  transition: all 0.2s ease;
}

.btn + .btn {
  margin-left: 10px;
}

.btn {
  display: inline-block;
  padding: 10px 15px;
  color: #fff;
  border-radius: 4px;
  border: none;
  background: #63c969;
  text-transform: uppercase;
  cursor: pointer;

  &.disabled {
    pointer-events: none;
    cursor: default;
    background: rgb(202, 202, 202);
  }
}

.btn-blue {
  background: #1f83ff;
}

.btn-red {
  background: #ec5050;
}

.btn-white {
  background: #fff;
  color: #333;
  border: 1px solid #ddd;
}

// Modal
.modal {
  position: absolute;
  top: 100%;
  right: 25px;
  z-index: 2;
  background: #fff;
  box-shadow: 0px 0px 15px #ddd;
  text-align: left;
  min-width: 300px;
  display: none;
  
  &.open {
    display: block;
  }

  &__title {
    font-size: 16px;
    color: #000;
  }

  &__header {
    padding: 15px 20px;
    border-bottom: 1px solid #ddd;
  }

  &__footer {
    padding: 10px 20px;
  }
}

</style>
