
<script>
import VueTournamentBracket from 'vue-tournament-bracket';

export default {
  components: {
    VueTournamentBracket,
  },
  data() {
    return {
      rounds: [
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
    };
  }
};
</script>


<template>
  <div>
    <vue-tournament-bracket :rounds="rounds">
      <template v-slot:player="{ player }">
        {{ player.name }}
      </template>
    </vue-tournament-bracket>
  </div>
</template>
