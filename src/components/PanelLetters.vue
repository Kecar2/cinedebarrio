
<script setup>
import { cleanLetter } from '@/utils/utils.js'
import { isSpecial } from '@/utils/utils.js'
</script>

<script>
export default {
  props: { "titleText": { type: String, required: true }, "guessedLetters": { type: Array, required: true } },
  computed: {
    title() {
      return this.titleText.split(" ");
    },
  },
};
</script>

<template>
  <div class="quest--panel">
    <!-- Bucle de palabras -->
    <span
      class="word--panel"
      v-for="(word, index) in title"
      :key="index"
    >
      <!-- Bucle de letras -->
      <span
        class="letter--panel"
        :class="{ empty: letter === ' ' }"
        v-for="(letter, index2) in word"
        :key="index2"
      >
        <TransitionGroup name="slide-fade">
          <!-- Letra con letra -->
          <span
            class="letter"
            :class="
              guessedLetters.includes(cleanLetter(letter)) || isSpecial(letter) ? 'animation' : ''
            "
            v-if="guessedLetters.includes(cleanLetter(letter)) || isSpecial(letter)"
          >
            {{ letter }}</span>
          <!-- Letra sin letra o espacio -->
          <span
            class="letter"
            v-if="!guessedLetters.includes(cleanLetter(letter)) && !isSpecial(letter)"
          />
        </TransitionGroup>
      </span>
    </span>
  </div>
</template>

<style scoped>
.empty {
  background-color: transparent;
  border: none;
}

.quest--panel {
  margin-top: 28px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.word--panel {
  display: flex;
  text-transform: uppercase;
  flex-wrap: nowrap;
  margin-left: 72px;
  margin-right: 72px;
  margin-top: 10px;
  justify-content: center;
  align-items: bottom;
}

.letter {
  display: flex;
  justify-content: center;
  align-items: center;
  text-transform: uppercase;
  font-size: 60px;
  border: black solid 1px;
  background-color: white;
  color: black;
  width: 80px;
  height: 80px;
  text-align: center;
  font-weight: 700;
  transition: 1s all;
  position: absolute;
  user-select: none;

}

.letter--panel {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  background-image: url("/panel-1letters.png");
  background-size: 100%;
  width: 145px;
  height: 171px;
  margin: -4px;

}

/*.animation {
  animation-name: animation;
  animation-duration: 1s;
    
}

@keyframes animation {
  from { transform: rotateY(-90deg);}
  to { transform: rotateY(0deg);}
}*/

/* Animacion */
.slide-fade-enter-active {
  transition: all 1s;
}

.slide-fade-leave-active {
  transition: all 0.5s;
}

.slide-fade-enter-from {
  opacity: 1;
  transform: rotateY(-90deg);
}

.slide-fade-leave-to {
  opacity: 0;
  transform: rotateY(0deg);
}

@media (max-width: 415px) {

  .letter--panel {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    background-image: url("/panel-1letters.png");
    background-size: 100%;
    width: 65px;
    height: 64px;
    margin: -4px;

  }

  .letter {
    margin-top: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
    text-transform: uppercase;
    font-size: 20px;
    border: black solid 1px;
    background-color: white;
    color: black;
    width: 30px;
    height: 30px;
    text-align: center;
    font-weight: 700;
    transition: 1s all;
    position: absolute;
    user-select: none;

  }

  .quest--panel {
    margin-top: 28px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  .word--panel {
    display: flex;
    text-transform: uppercase;
    flex-wrap: nowrap;
    margin-left: 72px;
    margin-right: 72px;
    justify-content: center;
    align-items: center;
    padding-bottom: 5px;
  }



}
</style>