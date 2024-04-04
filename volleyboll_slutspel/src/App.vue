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
       // Data om turneringen för spelare/lag i bracketsen
      rounds: [
      {
          games: [
            {
              // Datan inom bracketsen
              player1: { id: "1", name: "Deltagare 1", winner: "not-started" },
              player2: { id: "4", name: "Deltagare 4", winner: false },
            },
            {
              player1: { id: "5", name: "Deltagare 5", winner: false },
              player2: { id: "8", name: "Deltagare 8", winner: true },
            },
            {
              player1: { id: "10", name: "Deltagare 10", winner: false },
              player2: { id: "12", name: "Deltagare 12", winner: true },
            },
            {
              player1: { id: "10", name: "Deltagare 10", winner: false },
              player2: { id: "12", name: "Deltagare 12", winner: true },
            }
          ]
        },  
      {
          games: [
            {
              player1: { id: "1", name: "Deltagare 1", winner: false },
              player2: { id: "4", name: "Deltagare 4", winner: true },
            },
            {
              player1: { id: "5", name: "Deltagare 5", winner: false },
              player2: { id: "8", name: "Deltagare 8", winner: true },
            }
          ]
        },
        {
          games: [
            {
              player1: { id: "4", name: "Deltagare 4", winner: false },
              player2: { id: "8", name: "Deltagare 8", winner: true },
            }
          ]
        }
        
      ]
    }
    ;
  },
  methods: {
    getPlayerClass(player) {
    },
    toggleDropdown(player) {
      // Stäng alla dropdown förutom den som klickades
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
      // byt dropdown om man öppnar ny
      player.showDropdown = !player.showDropdown;
      // sätt text beroende på dropdown
      switch (player.id) {
        case "1":
          player.specialText = "Text ID 1";
          break;
        case "4":
          player.specialText = "Text ID 4";
          break;

        default:
          player.specialText = "Ingen information";
          break;
      }
    },
    closeDropdownsOnClickOutside(event) {
      // Stäng dropdown om klick utanför dem
      if (!this.$el.contains(event.target)) {
        this.rounds.forEach(round => {
          round.games.forEach(game => {
            game.player1.showDropdown = false;
            game.player2.showDropdown = false;
          });
        });
      }
    }
  },
  mounted() {
    document.addEventListener("click", this.closeDropdownsOnClickOutside);
  },
  beforeDestroy() {
    document.removeEventListener("click", this.closeDropdownsOnClickOutside);
  }
}
</script>

<template>
  <div class="nav">
    <div class="logo">
      <img class="volleyimg" src="@/assets/volleyboll.png">
    </div>

  </div>
  <vue-tournament-bracket :rounds="rounds">
    <template v-slot:player="{ player }">
      <div class="popup-trigger" @click="toggleDropdown(player)">
        <span :class="getPlayerClass(player)">
          {{ player.name }}
        </span>
      </div>
      <div v-if="player.showDropdown" class="dropdown">
        <p>{{ player.specialText }}</p>
      </div>
    </template>
  </vue-tournament-bracket>
</template>



<style>

.nav {
  background-color: blue;
  position:fixed;
  top:0%;
  left:0%;
  right:0%;
  height:3.5em;
  border: solid black;
  z-index:100;
}

.volleyimg {
  position:fixed;
  z-index:150;
  height:3.2em;
  width:3.2em;
}

.logo {
  background-color:black;
  position:fixed;
  z-index:150;
  height:3.2em;
  width:3.2em;
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
  bottom:30%!important;
  left:5%;
}
.vtb-item-players .not-started {
  background-color: gray !important;
}
.vtb-item-players, .vtb-item-players .winner, .vtb-item-players .defeated, .popup-trigger {
  width:15em;
}
.vtb-item-players .winner {
  background-color: greenyellow !important;
}
.vtb-item-players .defeated {
  background-color: red !important;
}
@media only screen and (max-height:400px){
  .vtb-wrapper{
    top: 45%;
  }
}
</style>
