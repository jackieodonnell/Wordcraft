<template>
  <div class="sidebar">    
    <ul v-for="word in correctWords" v-bind:key="word" id="correct-words">
        {{ word }}
    </ul>
    <ul v-for="guess in guessedWords" v-bind:key="guess" id="guessed-words">
        {{ guess }}
    </ul>

  </div>
</template>

<script>
export default {
    name: "sidebar-list",
    props: ["correctWords", "guessedWords"],
}
</script>

<style scoped>

.sidebar {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 1.2rem;
  font-weight: 600;
  color: rgba(63, 63, 63, 0.777);
}

.sidebar ul {
  margin-block-start: 2px;
  margin-block-end: 2px;
  padding-inline-start: 5%;
}

#correct-words {
  color: rgb(2, 176, 74);
}

</style>