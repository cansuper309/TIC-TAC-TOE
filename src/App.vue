<template>
  <div id="app">
    <Board />
  </div>
</template>

<script>
import Board from './components/Board.vue';

export default {
  name: 'App',
  components: {
    Board
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.board-row:after {
  clear: both;
  content: "";
  display: table;
}

.status {
  margin-bottom: 10px;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.square:focus {
  outline: none;
}

.kbd-navigation .square:focus {
  background: #ddd;
}

.board-container {
  display: inline-block;
  position: relative;
}

.board {
  position: relative;
}

.line {
  position: absolute;
  background-color: red;
  height: 3px;
  width: 102px;
  transform-origin: left;
}

.line-h-1 { top: 15.5px; }
.line-h-2 { top: 49.5px; }
.line-h-3 { top: 83.5px; }

.line-v-1 { top: 49.5px; left: -33px; transform: rotate(90deg); }
.line-v-2 { top: 49.5px; left: 1px; transform: rotate(90deg); }
.line-v-3 { top: 49.5px; left: 35px; transform: rotate(90deg); }

.line-d-1 { top: 0px; left: 0px; width: 125px; transform: rotate(45deg); transform-origin: top left; }
.line-d-2 { top: 0px; right: -1px; width: 125px; transform: rotate(-45deg); transform-origin: top right; }
</style>
