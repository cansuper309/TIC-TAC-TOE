<template>
  <div class="board-container">
    <div class="status">{{ status }}</div>
    <div class="board">
      <div class="board-row" v-for="i in 3" :key="i">
        <Square
          v-for="j in 3"
          :key="j"
          :value="squares[(i - 1) * 3 + (j - 1)]"
          @click="handleClick((i - 1) * 3 + (j - 1))"
        />
      </div>
      <div v-if="winner" :class="['line', lineClass]"></div>
    </div>
  </div>
</template>

<script>
import Square from './Square.vue';

export default {
  components: {
    Square
  },
  data() {
    return {
      squares: Array(9).fill(null),
      xIsNext: true,
      winner: null,
      lineClass: ''
    };
  },
  computed: {
    status() {
      if (this.winner) {
        return 'Winner: ' + this.winner.winner;
      } else {
        return 'Next player: ' + (this.xIsNext ? 'X' : 'O');
      }
    }
  },
  methods: {
    handleClick(i) {
      if (this.winner || this.squares[i]) {
        return;
      }
      const squares = this.squares.slice();
      squares[i] = this.xIsNext ? 'X' : 'O';
      this.squares = squares;
      this.xIsNext = !this.xIsNext;
      this.winner = this.calculateWinner(this.squares);
      if (this.winner) {
        this.lineClass = this.getLineClass(this.winner.line);
      }
    },
    calculateWinner(squares) {
      const lines = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8], // rows
        [0, 3, 6], [1, 4, 7], [2, 5, 8], // columns
        [0, 4, 8], [2, 4, 6]             // diagonals
      ];
      for (let i = 0; i < lines.length; i++) {
        const [a, b, c] = lines[i];
        if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
          return { winner: squares[a], line: lines[i] };
        }
      }
      return null;
    },
    getLineClass(line) {
      if (line.join('') === '012') return 'line-h-1';
      if (line.join('') === '345') return 'line-h-2';
      if (line.join('') === '678') return 'line-h-3';
      if (line.join('') === '036') return 'line-v-1';
      if (line.join('') === '147') return 'line-v-2';
      if (line.join('') === '258') return 'line-v-3';
      if (line.join('') === '048') return 'line-d-1';
      if (line.join('') === '246') return 'line-d-2';
      return '';
    }
  }
};
</script>
