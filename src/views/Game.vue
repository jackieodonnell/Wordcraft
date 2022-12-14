<template>
  <div class="game">
    <div class="btn-header">
      <button id="directions-btn" v-on:click="toggleDirections()">
        How To Play
      </button>
      <button id="start-btn" v-on:click="newGame">New Game</button>
    </div>
    <div class="directions-popup" v-if="displayDirections">
      <h2>How To Play</h2>
      <p>
        The game board contains four 5-letter words that have been scrambled
        into columns. You must use one letter from each column to create
        5-letter words.
      </p>
      <p>
        If your guess is one of the scrambled words, those letters will turn
        <span id="green-txt">green</span>.
      </p>
      <p>
        If your guess is not one of the scrambled words, those letters will turn
        <span id="gray-txt">gray</span>.
      </p>
      <p>
        The goal is to use all of the letters on the board in as few words as
        possible. Good luck!
      </p>
      <button id="close-btn" v-on:click="toggleDirections()">CLOSE</button>
    </div>
    <word-list />
    <div id="game-board">
      <div id="btn-header">
        <button id="clear-btn" v-on:click="clearAnswer">Clear</button>
        <button id="submit-btn" v-on:click="submitWord">Submit</button>
      </div>

      <div id="word-guess">
        <letter-space id="one" v-bind:spaceNumber="1" />
        <letter-space id="two" v-bind:spaceNumber="2" />
        <letter-space id="three" v-bind:spaceNumber="3" />
        <letter-space id="four" v-bind:spaceNumber="4" />
        <letter-space id="five" v-bind:spaceNumber="5" />
        <letter-set
          id="set1"
          v-bind:setNumber="1"
          v-bind:isSubmitted="isSubmitted"
        />
        <letter-set
          id="set2"
          v-bind:setNumber="2"
          v-bind:isSubmitted="isSubmitted"
        />
        <letter-set
          id="set3"
          v-bind:setNumber="3"
          v-bind:isSubmitted="isSubmitted"
        />
        <letter-set
          id="set4"
          v-bind:setNumber="4"
          v-bind:isSubmitted="isSubmitted"
        />
        <letter-set
          id="set5"
          v-bind:setNumber="5"
          v-bind:isSubmitted="isSubmitted"
        />
      </div>

      <div id="guesses">
        <h2 id="words-found-header">WORDS FOUND:</h2>
        <sidebar-list
          v-bind:correctWords="correctWords"
          v-bind:guessedWords="guessedWords"
        />
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import LetterSet from "@/components/LetterSet.vue";
import LetterSpace from "@/components/LetterSpace.vue";
import WordList from "@/components/WordList.vue";
import SidebarList from "../components/Sidebar.vue";

export default {
  name: "GameBoard",
  components: {
    LetterSet,
    LetterSpace,
    WordList,
    SidebarList,
  },
  data() {
    return {
      displayGame: false,
      correctWords: [],
      guessedWords: [],
      isSubmitted: false,
      displayDirections: false,
    };
  },
  computed: {
    fourWords() {
      return this.$store.state.selectedWords;
    },
  },
  methods: {
    toggleDisplayBtn() {
      if (this.displayGame) {
        this.displayGame = false;
      } else {
        this.displayGame = true;
      }
    },
    newGame() {
      this.$router.go();
    },
    clearAnswer() {
      this.$store.commit("SET_SELECTION_1", "");
      this.$store.commit("SET_SELECTION_2", "");
      this.$store.commit("SET_SELECTION_3", "");
      this.$store.commit("SET_SELECTION_4", "");
      this.$store.commit("SET_SELECTION_5", "");
      this.isSubmitted = true;
    },
    submitWord() {
      let inputWord =
        this.$store.state.selectedLetter1 +
        this.$store.state.selectedLetter2 +
        this.$store.state.selectedLetter3 +
        this.$store.state.selectedLetter4 +
        this.$store.state.selectedLetter5;
      if (
        this.guessedWords.includes(inputWord) ||
        this.correctWords.includes(inputWord)
      ) {
        alert("You've already guessed this word!");
        this.clearAnswer();
      } else if (this.$store.state.selectedWords.includes(inputWord)) {
        this.correctWords.push(inputWord);
        this.$store.commit("SET_CORRECT_WORDS", this.correctWords);
        this.clearAnswer();
      } else if (this.$store.state.wordList.includes(inputWord)) {
        this.guessedWords.push(inputWord);
        this.$store.commit("SET_GUESSED_WORDS", this.guessedWords);
        this.clearAnswer();
      } else {
        alert("Invalid Word Entry!");
        this.clearAnswer();
      }
    },
    toggleDirections() {
      if (!this.displayDirections) {
        this.displayDirections = true;
      } else {
        this.displayDirections = false;
      }
    },
  },
};
</script>

<style scoped>
.game {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
}

#start-btn,
#directions-btn {
  height: fit-content;
  margin-top: 10px;
  padding: 8px;
  width: 160px;
  font-weight: 600;
  font-size: 1rem;
  text-transform: uppercase;
  border: 1.5px solid rgba(135, 135, 135, 0.501);
  border-radius: 4px;
  background-color: rgb(239, 246, 255);
  box-shadow: 0 8px 12px 0 rgb(16 39 112 / 10%);
}
#start-btn:hover {
  background-color: white;
}
#directions-btn {
  background-color: rgb(255, 248, 224);
}
#directions-btn:hover {
  background-color: white;
}

.directions-popup {
  background-color: white;
  border: 1px solid gray;
  box-shadow: 0 8px 12px 0 rgb(16 39 112 / 10%);
  border-radius: 10px;
  position: absolute;
  width: fit-content;
  height: fit-content;
  min-width: 320px;
  padding: 20px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.directions-popup h2 {
  font-weight: 600;
  text-transform: uppercase;
}

.directions-popup p {
  font-size: 1.2rem;
  text-align: left;
  font-weight: 500;
}

#green-txt {
  color: #1aa92dfd;
  font-weight: 800;
}

#gray-txt {
  color: #676765;
  font-weight: 800;
}

#close-btn {
  height: fit-content;
  margin-top: 0%;
  padding: 5px;
  width: 35%;
  border: 1.5px solid rgba(135, 135, 135, 0.501);
  border-radius: 4px;
  background-color: rgb(255, 248, 224);
  box-shadow: 0 8px 12px 0 rgb(16 39 112 / 10%);
  font-weight: 600;
  text-transform: uppercase;
}
#close-btn:hover {
  background-color: rgb(255, 233, 153);
}

#btn-header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-top: 10%;
}

#word-guess {
  display: grid;
  height: fit-content;
  margin-top: 3%;
  margin-left: 0px;
  width: fit-content;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
  grid-template-rows: 20% 90%;
  grid-template-areas:
    "one two three four five"
    "set1 set2 set3 set4 set5";
  justify-items: center;
}

#one,
#two,
#three,
#four,
#five {
  border-bottom: 2px solid rgba(0, 0, 0, 0.676);
  height: 65px;
  width: 50px;
  font-size: 1.1rem;
}

#one {
  grid-area: one;
}
#two {
  grid-area: two;
}
#three {
  grid-area: three;
}
#four {
  grid-area: four;
}
#five {
  grid-area: five;
}
#set1 {
  grid-area: set1;
}
#set2 {
  grid-area: set2;
}
#set3 {
  grid-area: set3;
}
#set4 {
  grid-area: set4;
}
#set5 {
  grid-area: set5;
}
#clear-btn {
  grid-area: clearbtn;
  height: fit-content;
  margin-top: 0%;
  padding: 5px;
  width: 35%;
  border: 1.5px solid rgba(135, 135, 135, 0.501);
  border-radius: 4px;
  background-color: rgba(236, 138, 138, 0.673);
  box-shadow: 0 8px 12px 0 rgb(16 39 112 / 10%);
  font-weight: 600;
  text-transform: uppercase;
}
#clear-btn:hover {
  background-color: rgba(242, 87, 87, 0.826);
}
#submit-btn {
  grid-area: submit;
  height: fit-content;
  margin-top: 0%;
  padding: 5px;
  width: 35%;
  border: 1.5px solid rgba(135, 135, 135, 0.501);
  border-radius: 4px;
  background-color: rgba(158, 236, 148, 0.673);
  box-shadow: 0 8px 12px 0 rgb(16 39 112 / 10%);
  font-weight: 600;
  text-transform: uppercase;
}
#submit-btn:hover {
  background-color: rgba(108, 240, 101, 0.826);
}

#guesses {
  grid-area: guesses;
}

#words-found-header {
  font-family: Arial, Helvetica, sans-serif;
  font-weight: 300;
  font-size: 1.2rem;
  border-bottom: 1px solid gray;
  margin-top: 40px;
}
</style>
