
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
    toggleDropdown(player) {
      // stäng ner den första dropdownen när man öppnar en ny
      this.rounds.forEach(round => {
        round.games.forEach(game => {
          if (game.player1 !== player && game.player1.showDropdown) {
            game.player1.showDropdown = false;
          }
          if (game.player2 !== player && game.player2.showDropdown) {
            game.player2.showDropdown = false;
          }
        });
      });
      // Ttoggle dropdown
      player.showDropdown = !player.showDropdown;
      // speciel text med id
      switch (player.id) {
        case "1":
          player.specialText = "Text ID 1";
          break;
        case "4":
          player.specialText = "Text ID 4";
          break;
        // om det inte finns inte information
        default:
          player.specialText = "No information";
          break;
      }
    }
  }
}
</script>


<template>
  <div class="container">
    <vue-tournament-bracket :rounds="rounds">
      <template v-slot:player="{ player }">
        <span :class="getPlayerClass(player)" @click="toggleDropdown(player)">
          {{ player.name }}
        </span>
        <div v-if="player.showDropdown" class="dropdown">
          <p>{{ player.specialText }}</p>
        </div>
      </template>
    </vue-tournament-bracket>
  </div>
</template>


<style>
.container {
  display: flex;
}

.dropdown {
  position: absolute;
  background-color: black; 
  color: white;
  min-width: 160px;
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
  padding: 12px 16px;
  z-index: 1;
}

.dropdown p {
  background-color: black !important;
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
