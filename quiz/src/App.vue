<script setup>
import { ref, computed } from 'vue'

//Fragen & Antwortmöglichkeiten
const questions = ref([
  {
	question: 'Wie entsehen Ebbe und Flut?',
	answer: 1,
	options: [
		'Die Gezeiten entstehen, weil 🐠 im Ozean Tango tanzen und dabei das Wasser durcheinanderwirbeln.',
		'Gezeiten sind Meeresspiegelschwankungen, ausgelöst durch die Gravitation von ☀️ und 🌕. Es gibt zwei Hauptgezeiten täglich - Hochwasser und Niedrigwasser.',
		'Gezeiten sind das Ergebnis davon, dass 🐋 im Meer Hula-Hoop spielen und dabei versehentlich Wellen erzeugen.'
	],
	selected: null
  },

  {
	question: 'Welche wichtige Funktion erfüllt das Wattenmeer in der Nordsee?',
	answer: 0,
	options: [
		'Das Wattenmeer dient als wichtiger Lebensraum für eine Vielzahl von Meereslebewesen 🐡🦈🧜🏻',
		'Das Wattenmeer ist ein gigantisches Trampolin für springende 🐟',
		'Das Wattenmeer ist der geheime Trainingsplatz für 🦑-Marathons.'
	],
	selected: null
  },

  {
	question: 'Welche Gefahr droht Schiffen in der Nordsee oft durch das Wetter?',
	answer: 0,
	options: [
		'Stürmische 💨 und hohe 🌊 können die Navigation erschweren.',
		'Die Nordsee ist berüchtigt für fliegende Piratenmöwen, die 🚢 überfallen.',
		'In der Nordsee gibt es regelmäßige 🌪️-Wettbewerbe für Schiffe, die nach dem besten Wellenritt suchen.'
	],
	selected: null
  }
])

const quizCompleted = ref(false)
const currentQuestion = ref(0)

//Berechnung der Punktzahl
const score = computed(() => {
	let value = 0
	questions.value.map(q => {
		if (q.selected != null && q.answer == q.selected) {
			console.log('richtig');
			value++
		}
	})
	return value
})
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
