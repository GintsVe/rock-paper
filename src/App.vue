<template>
  <div class="game-wrapper">
    <div class="buttons">
      <Button @click="reset()" title="Reset" />
      <Button @click="toggleModal()" title="Winning Conditions" />
    </div>
    <div class="game-window">
      <div class="score">
        <h2 class="heading2">Player score: {{ player.score }}</h2>
        <h2 class="heading2">Computer score: {{ cpu.score }}</h2>
      </div>
      <SelectedWeapons :cpu="cpu" :player="player" />
      <Winner :winner="winner" />
      <div class="options">
        <div class="option" v-for="(option, index) in options" :key="option">
          <img
            class="image"
            :src="option.img"
            @click="chooseWeapons(index)"
            :alt="option.weapon"
          />
        </div>
      </div>
    </div>
  </div>
  <div
    :style="[modalOpen ? { display: 'block' } : { display: 'none' }]"
    class="modal"
  >
    <div class="modal__content">
      <div v-for="{ winner, looser } in winningOptions" :key="winner + looser">
        <h2 class="heading2">{{ winner }} wins {{ looser }}</h2>
      </div>
      <Button @click="toggleModal()" title="Close" />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import SelectedWeapons from "@/components/SelectedWeapons.vue";
import Winner from "@/components/Winner.vue";
import Button from "@/components/Button.vue";

export default defineComponent({
  name: "App",
  components: {
    SelectedWeapons,
    Winner,
    Button,
  },
  data: () => ({
    player: {
      score: 0,
      selected: { weapon: "", img: "" },
    },
    cpu: {
      score: 0,
      selected: { weapon: "", img: "" },
    },
    options: [
      { weapon: "Rock", img: require(`@/assets/images/rock.jpg`) },
      { weapon: "Paper", img: require("./assets/images/paper.jpg") },
      { weapon: "Scissors", img: require("./assets/images/scissors.jpg") },
      { weapon: "Lizard", img: require("./assets/images/lizard.jpg") },
      { weapon: "Spock", img: require("./assets/images/spock.png") },
    ],
    winningOptions: [
      { winner: "Rock", looser: "Scissors" },
      { winner: "Rock", looser: "Lizard" },
      { winner: "Scissors", looser: "Paper" },
      { winner: "Scissors", looser: "Lizard" },
      { winner: "Paper", looser: "Rock" },
      { winner: "Paper", looser: "Spock" },
      { winner: "Lizard", looser: "Spock" },
      { winner: "Lizard", looser: "Paper" },
      { winner: "Spock", looser: "Scissors" },
      { winner: "Spock", looser: "Rock" },
    ],
    winner: "",
    modalOpen: false,
  }),
  methods: {
    chooseWeapons(index: number) {
      this.player.selected = this.options[index];
      this.cpu.selected = this.options[Math.floor(Math.random() * 5)];
      this.setWinner();
    },
    setWinner() {
      const playerWeapon = this.player.selected.weapon;
      const cpuWeapon = this.cpu.selected.weapon;

      if (playerWeapon === cpuWeapon) {
        this.winner = "Tie";
      } else if (
        this.winningOptions.find(
          ({ winner, looser }) =>
            winner === playerWeapon && looser === cpuWeapon
        )
      ) {
        this.winner = "Player";
        this.player.score++;
      } else {
        this.winner = "Computer";
        this.cpu.score++;
      }
    },
    toggleModal() {
      this.modalOpen = !this.modalOpen;
    },
    reset() {
      this.player = {
        score: 0,
        selected: { weapon: "", img: "" },
      };

      this.cpu = {
        score: 0,
        selected: { weapon: "", img: "" },
      };

      this.winner = "";
    },
  },
});
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Inter&display=swap");

* {
  box-sizing: border-box;
}

body {
  background-image: url("assets/images/background.png");
  background-color: antiquewhite;
  background-repeat: no-repeat;
  background-size: cover;
}

.game-wrapper {
  padding: 10px;
  gap: 10px;
  margin: auto auto;
  max-width: 1100px;
  width: 100%;
  max-height: 800px;
  height: 100%;
  display: flex;
  flex-direction: column;
}

.game-window {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 50px;
  border: 1px solid black;
  border-radius: 20px;
  padding: 50px;
  background-color: rgba(0, 0, 0, 0.1);
}

.option {
  width: 150px;
  height: 150px;
  background-color: white;
  border-radius: 50%;
  box-shadow: rgba(0, 0, 0, 0.24) 0 3px 8px;
  cursor: pointer;
  transition: 0.5s;

  &:hover {
    transform: scale(1.2);
  }
}

.option--size {
  width: 200px;
  height: 200px;
}

.image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
}

.options {
  display: flex;
  justify-content: space-around;
}

.score {
  display: flex;
  justify-content: space-around;
}

.heading2 {
  font-size: 24px;
  font-family: "Inter", sans-serif;
}

.buttons {
  margin: 0 auto;
  max-width: 1100px;
  width: 100%;
  display: flex;
  justify-content: space-around;
}

.modal {
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  animation: fadein 0.7s;
}

.modal__content {
  background-color: #fefefe;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  max-width: 500px;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

@keyframes fadein {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
