<script setup lang="ts">

interface GameLog {
  row: number,
  col: number,
}

const gameLogs = ref<GameLog[]>([])

function onClick(row: number, col: number) {
  gameLogs.value.push({
    row, col
  })

  let player1: GameLog[] = []
  let player2: GameLog[] = []
  gameLogs.value.forEach((item, index) => {
    if (index % 2 === 0) {
      player1.push(item)
    } else {
      player2.push(item)
    }
  })

  console.log('player1 :>> ', player1);
  console.log('player2 :>> ', player2);
}

function pieces(row: number, col: number) {

  const index = gameLogs.value.findIndex(item => (item.row === row && item.col === col))
  if (index === -1) {
    return ''
  }

  if (index % 2 === 0) {
    return 'i-carbon:radio-button'
  }
  // 'i-carbon:radio-button'
  return 'i-carbon:close'
}

</script>

<template>
  <div flex="~" justify-center>
    <div>
      <div v-for="row in 3" flex="~">
        <div v-for="col in 3" w-20 h-20 border-1 text-5xl flex="~" justify-center items-center
          @click="onClick(row, col)">
          <div :class="pieces(row, col)"></div>
        </div>
      </div>
    </div>
  </div>
</template>
