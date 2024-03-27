
<script>
// Importera vue-tournament-bracket
import VueTournamentBracket from 'vue-tournament-bracket';

export default {
  components: {
     // Registrera VueTournamentBracket
    VueTournamentBracket,
  },
  data() {
    return {
       // Data om turnenringaran för players/teams i bracketsen
      rounds: [
      {
          games: [
            {
              // Datan inom bracketsen
              player1: { id: "1", name: "Competitor 1", winner: "not-started" },
              player2: { id: "4", name: "Competitor 4", winner: false },
            },
            {
              player1: { id: "5", name: "Competitor 5", winner: false },
              player2: { id: "8", name: "Competitor 8", winner: true },
            },
            {
              player1: { id: "10", name: "Competitor 10", winner: false },
              player2: { id: "12", name: "Competitor 12", winner: true },
            },
            {
              player1: { id: "10", name: "Competitor 10", winner: false },
              player2: { id: "12", name: "Competitor 12", winner: true },
            }
          ]
        },  
      {
          games: [
            {
              player1: { id: "1", name: "Competitor 1", winner: false },
              player2: { id: "4", name: "Competitor 4", winner: true },
            },
            {
              player1: { id: "5", name: "Competitor 5", winner: false },
              player2: { id: "8", name: "Competitor 8", winner: true },
            }
          ]
        },
        {
          games: [
            {
              player1: { id: "4", name: "Competitor 4", winner: false },
              player2: { id: "8", name: "Competitor 8", winner: true },
            }
          ]
        }
        
      ]
    }
    ;
  },
  methods: {
  getPlayerClass(player) {
    if (player.winner === true) {
      return 'winner';
    } else if (player.winner === false) {
      return 'loser';
    } else {
      return 'not-started';
    }
  }
}
}

</script>


<template>
  <div class="container">
    <!-- visa vad som finns i bracketseb -->
    <vue-tournament-bracket :rounds="rounds">
      <!-- visa namnen på spelare -->
      <template v-slot:player="{ player }">
        <span :class="getPlayerClass(player)">{{ player.name }}</span>
      </template>
    </vue-tournament-bracket>
  </div>
</template>


<style>
.container {
  display: flex;
}

.vtb-wrapper {
  position: relative; 
  left: 50%;
}


.vtb-item-players .not-started {
  background-color: gray !important;
}

.vtb-item-players .winner {
  background-color: greenyellow !important;
}

.vtb-item-players .defeated {
  background-color: red !important;
}

</style>