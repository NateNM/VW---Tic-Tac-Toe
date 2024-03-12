<template>
  <div v-if="!gameOver" id="board">
    <div class="square" v-for="n in 9" :key="n" @click="clickedSquare(n)">
      {{ square[n] }}
    </div>
  </div>
</template>

<script>

import { ref } from "vue";

export default {
  name: 'App',
  setup() {
    let square = ref([]);
    let currentTurn = "X"
    let gameOver = ref(false)

    for (let i = 0; i<=9; i++) {
      square.value.push("empty");
    }
    
    function clickedSquare(n) {
      if (square.value[n] !== "empty") return;
      
      isWinner();
      isCat();

      square.value[n] = currentTurn;
      currentTurn === "X" ? (currentTurn="O") : (currentTurn = "X")
      console.log(currentTurn)
      console.log(gameOver)
    }

    function isWinner() {
      const lines = [
        [1,2,3],
        [4,5,6],
        [7,8,9],
        [1,4,7],
        [2,4,8],
        [3,6,9],
        [1,5,9],
        [3,5,7]
      ]
      for(let i=0;i<lines.length;i++) {
        const [a,b,c] = lines[i]

        if (square.value[a] !== "empty" && square.value[a] === square.value[b] && square.value[a] === square.value[c])
          gameOver.value = true;
      }    
    }

    function isCat() {
      let isCats = true;
      square.value.forEach((s) => {
        if(s==="empty") 
          isCats = false;
      });
      if (isCats == true) 
        gameOver.value = true;
    }

    return {square, clickedSquare, gameOver}
  }
}
</script>

<style>
#board{
  height: 400px;
  width: 400px;
  margin: 0 auto;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.square {
  width: 30%;
  background-color: grey;
  border: 1px solid black;
}


</style>
