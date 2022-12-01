<template>
  <div
    class="letter-box"
    @click="
      $emit('click');
      toggleHighlight();
    "
    v-bind:class="{
      highlight: highlight,
      correct: isCorrect,
      submitted: isSubmitted,
    }"
  >
    <h1 class="letter">{{ letter }}</h1>
  </div>
</template>

<script>
export default {
  name: "letter-box",
  props: ["letter", "isCorrect", "isSubmitted"],
  data() {
    return {
      highlight: false,
    };
  },
  methods: {
    toggleHighlight() {
      if (!this.highlight && !this.isSubmitted) {
        this.highlight = true;
      } else {
        this.highlight = false;
      }
    },
  },
};
</script>

<style scoped>
.letter-box {
  background-color: rgba(246, 246, 246, 0.842);
  border: 1.5px solid rgba(135, 135, 135, 0.501);
  border-radius: 4px;
  width: 60px;
  height: 60px;
  margin-top: 2px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 8px 12px 0 rgb(16 39 112 / 10%);
  transition: all 0.1s ease-in-out;
}

.letter {
  color: rgba(44, 44, 44, 0.767);
  display: flex;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-weight: 500;
  font-size: 3rem;
  text-transform: uppercase;
}

.letter-box:hover {
  background-color: #58c7ffd0;
  box-shadow: 0 8px 24px 0 rgb(16 39 112 / 50%);
}

.submitted {
  background-color: #aba9a0d5;
}
/* .highlight {
  background-color: #58c7ffd0;
} */

.correct {
  background-color: #7ff48fd5;
}
</style>
