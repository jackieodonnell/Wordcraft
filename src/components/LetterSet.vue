<template>
  <div class="letter-set">
    <letter-box id="choice1" v-bind:letter="choice1" v-bind:isCorrect="highlight1" v-bind:isSubmitted="guessed1" @click="toggleSelection(choice1)"/>
    <letter-box id="choice2" v-bind:letter="choice2" v-bind:isCorrect="highlight2" v-bind:isSubmitted="guessed2" @click="toggleSelection(choice2)"/>
    <letter-box id="choice3" v-bind:letter="choice3" v-bind:isCorrect="highlight3" v-bind:isSubmitted="guessed3" @click="toggleSelection(choice3)"/>
  </div>
</template>

<script>
import LetterBox from './LetterBox.vue';
export default {
  components: { LetterBox },
    name: "letter-set",
    props: ["setNumber", "isSubmitted"],
    data() {
        return {
            word: "",
            shuffledLetters: [],
            choice1: "",
            choice2: "",
            choice3: "",
            highlight1: false,
            highlight2: false,
            highlight3: false,
            guessed1: false,
            guessed2: false,
            guessed3: false
        }
    },
    computed: {
        correctCount(){
            return this.$store.state.correctWords.length;
        },
        guessedCount(){
            return this.$store.state.guessedWords.length;
        }
    },
    watch: {
        correctCount(newValue, oldValue){
            if (newValue > oldValue){            
                if (this.setNumber == 1){
                    const a1 = this.$store.state.correctWords[newValue - 1].substring(0,1);
                    if (a1 == this.choice1 && !this.highlight1){
                        this.highlight1 = true;
                    } else if (a1 == this.choice2  && !this.highlight2){
                        this.highlight2 = true;
                    } else if (a1 == this.choice3 && !this.highlight3){
                        this.highlight3 = true;
                    } 
                } else if (this.setNumber == 2){
                    const a2 = this.$store.state.correctWords[newValue - 1].substring(1,2);
                    if (a2 == this.choice1 && !this.highlight1){
                        this.highlight1 = true;
                    } else if (a2 == this.choice2  && !this.highlight2){
                        this.highlight2 = true;
                    } else if (a2 == this.choice3 && !this.highlight3){
                        this.highlight3 = true;
                    } 
                } else if (this.setNumber == 3){
                    const a3 = this.$store.state.correctWords[newValue - 1].substring(2,3);
                    if (a3 == this.choice1 && !this.highlight1){
                        this.highlight1 = true;
                    } else if (a3 == this.choice2  && !this.highlight2){
                        this.highlight2 = true;
                    } else if (a3 == this.choice3 && !this.highlight3){
                        this.highlight3 = true;
                    } 
                } else if (this.setNumber == 4){
                    const a4 = this.$store.state.correctWords[newValue - 1].substring(3,4);
                    if (a4 == this.choice1 && !this.highlight1){
                        this.highlight1 = true;
                    } else if (a4 == this.choice2  && !this.highlight2){
                        this.highlight2 = true;
                    } else if (a4 == this.choice3 && !this.highlight3){
                        this.highlight3 = true;
                    } 
                } else {
                    const a5 = this.$store.state.correctWords[newValue - 1].substring(4);
                    if (a5 == this.choice1 && !this.highlight1){
                        this.highlight1 = true;
                    } else if (a5 == this.choice2  && !this.highlight2){
                        this.highlight2 = true;
                    } else if (a5 == this.choice3 && !this.highlight3){
                        this.highlight3 = true;
                    } 
                }
            }
            return false;
        },
        guessedCount(newValue, oldValue){
            if (newValue > oldValue){            
                if (this.setNumber == 1){
                    const a1 = this.$store.state.guessedWords[newValue - 1].substring(0,1);
                    if (a1 == this.choice1 && !this.highlight1 && !this.guessed1){
                        this.guessed1 = true;
                    } else if (a1 == this.choice2  && !this.highlight2 && !this.guessed2){
                        this.guessed2 = true;
                    } else if (a1 == this.choice3 && !this.highlight3 && !this.guessed3){
                        this.guessed3 = true;
                    } 
                } else if (this.setNumber == 2){
                    const a2 = this.$store.state.guessedWords[newValue - 1].substring(1,2);
                    if (a2 == this.choice1 && !this.highlight1 && !this.guessed1){
                        this.guessed1 = true;
                    } else if (a2 == this.choice2  && !this.highlight2 && !this.guessed2){
                        this.guessed2 = true;
                    } else if (a2 == this.choice3 && !this.highlight3 && !this.guessed3){
                        this.guessed3 = true;
                    } 
                } else if (this.setNumber == 3){
                    const a3 = this.$store.state.guessedWords[newValue - 1].substring(2,3);
                    if (a3 == this.choice1 && !this.highlight1 && !this.guessed1){
                        this.guessed1 = true;
                    } else if (a3 == this.choice2  && !this.highlight2 && !this.guessed2){
                        this.guessed2 = true;
                    } else if (a3 == this.choice3 && !this.highlight3 && !this.guessed3){
                        this.guessed3 = true;
                    } 
                } else if (this.setNumber == 4){
                    const a4 = this.$store.state.guessedWords[newValue - 1].substring(3,4);
                    if (a4 == this.choice1 && !this.highlight1 && !this.guessed1){
                        this.guessed1 = true;
                    } else if (a4 == this.choice2  && !this.highlight2 && !this.guessed2){
                        this.guessed2 = true;
                    } else if (a4 == this.choice3 && !this.highlight3 && !this.guessed3){
                        this.guessed3 = true;
                    } 
                } else {
                    const a5 = this.$store.state.guessedWords[newValue - 1].substring(4);
                    if (a5 == this.choice1 && !this.highlight1 && !this.guessed1){
                        this.guessed1 = true;
                    } else if (a5 == this.choice2  && !this.highlight2 && !this.guessed2){
                        this.guessed2 = true;
                    } else if (a5 == this.choice3 && !this.highlight3 && !this.guessed3){
                        this.guessed3 = true;
                    } 
                }
            }
            return false;
        }
    },
    created() {
        let array = [];
        if (this.setNumber == 1){
            array = this.$store.state.letterSet1
        } else if (this.setNumber == 2){
            array = this.$store.state.letterSet2
        } else if (this.setNumber == 3){
            array = this.$store.state.letterSet3
        } else if (this.setNumber == 4){
            array = this.$store.state.letterSet4
        } else {
            array = this.$store.state.letterSet5
        }

        for (let i = array.length - 1; i > 0; i--) {
            let j = Math.floor(Math.random() * (i + 1));
            let temp = array[i];
            array[i] = array[j];
            array[j] = temp;
        }
        this.shuffledLetters = array;
        this.choice1 = this.shuffledLetters[0];
        this.choice2 = this.shuffledLetters[1];
        this.choice3 = this.shuffledLetters[2];
    },
    methods: {
        toggleSelection(choice){
            if (this.setNumber == 1){
                this.$store.commit('SET_SELECTION_1', choice)
            } else if (this.setNumber == 2){
                this.$store.commit('SET_SELECTION_2', choice)
            } else if (this.setNumber == 3){
                this.$store.commit('SET_SELECTION_3', choice)
            } else if (this.setNumber == 4){
                this.$store.commit('SET_SELECTION_4', choice)
            } else {
                this.$store.commit('SET_SELECTION_5', choice)
            }
            this.$emit('updateDisplayLetter', choice);
        }
    }

}
</script>

<style scoped>
.letter-set {
    display: flex;
    flex-direction: column;
    align-items: center;
}


</style>