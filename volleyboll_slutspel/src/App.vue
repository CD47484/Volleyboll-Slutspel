
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
              id:1,
              next:5,
              player1: { id: "1", name: "Competitor 1", winner: null },
              player2: { id: "4", name: "Competitor 4", winner: false },
            },
            {
              id:2,
              next:5,
              player1: { id: "5", name: "Competitor 5", winner: false },
              player2: { id: "8", name: "Competitor 8", winner: true },
            },
            {
              id:3,
              next:6,
              player1: { id: "10", name: "Competitor 10", winner: false },
              player2: { id: "12", name: "Competitor 12", winner: true },
            },
            {
              id:4,
              next:6,
              player1: { id: "10", name: "Competitor 10", winner: false },
              player2: { id: "12", name: "Competitor 12", winner: true },
            }
          ]
        },  
      {
          games: [
            {
              id:5,
              next:7,
              player1: { id: "1", name: "Competitor 1", winner: false },
              player2: { id: "4", name: "Competitor 4", winner: true },
            },
            {
              id:6,
              next:7,
              player1: { id: "5", name: "Competitor 5", winner: false },
              player2: { id: "8", name: "Competitor 8", winner: true },
            }
          ]
        },
        {
          games: [
            {
              id:7,
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
  position: absolute; 
  bottom:20%!important;
  left:5%;
  padding:0%;
}

.vtb-item-players .winner {
  background-color: greenyellow !important;
  
}

.vtb-item-players, .vtb-item-players .winner, .vtb-item-players .defeated {
  width:20em;
  

}

.vtb-item-players .defeated {
  background-color: red !important;
}

@media only screen and (max-height:400px){
  .vtb-wrapper{
    top: 55%;
  }
}

</style>