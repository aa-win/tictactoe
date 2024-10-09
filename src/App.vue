<template>
  <!-- Main container, centers content, full screen height -->
  <div class="min-h-screen bg-gray-100 flex items-center justify-center select-none">
    
    <!-- Wrapper for game content, centered with spacing -->
    <div class="text-center space-y-4">
      
      <!-- Game title -->
      <h1 class="text-4xl font-bold">Tic Tac Toe</h1>
      
      <!-- 3x3 Tic Tac Toe grid -->
      <div class="grid grid-cols-3 gap-2">
        
        <!-- v-for loop generates 9 buttons -->
        <button
          v-for="(cell, index) in board" 
          :key="index"
          @click="makeMove(index)"
          class="w-24 h-24 flex items-center justify-center bg-white border-2 border-gray-400 text-3xl font-bold hover:bg-gray-200 text-gray-800"
        >
          {{ cell }} <!-- Display cell value -->
        </button>
      </div>
      
      <!-- Show winner message -->
      <div v-if="winner" class="text-xl font-semibold">
        {{ winner }} Wins!
      </div>
      
      <!-- Reset button -->
      <button 
        @click="resetGame"
        class="mt-4 px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
      >
        Reset Game
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      board: Array(9).fill(''),  // 9 empty cells
      currentPlayer: 'X',        // Start with 'X'
      winner: null,              // No winner initially
    };
  },
  methods: {
    makeMove(index) {
      // Handle player move if cell is empty and no winner
      if (!this.board[index] && !this.winner) {
        this.board[index] = this.currentPlayer;  // Set current player's mark
        if (this.checkWinner()) {                // Check if current player won
          this.winner = this.currentPlayer;
        } else {
          // Switch between 'X' and 'O'
          this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
        }
      }
    },
    checkWinner() {
      // Winning combinations
      const combos = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
        [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
        [0, 4, 8], [2, 4, 6],            // Diagonals
      ];
      // Return true if any combo matches
      return combos.some(combo => 
        this.board[combo[0]] &&
        this.board[combo[0]] === this.board[combo[1]] &&
        this.board[combo[1]] === this.board[combo[2]]
      );
    },
    resetGame() {
      // Reset game state
      this.board = Array(9).fill('');  // Clear board
      this.currentPlayer = 'X';        // Reset to 'X'
      this.winner = null;              // Clear winner
    }
  }
};
</script>

<style scoped>
/* Custom styles */
</style>
