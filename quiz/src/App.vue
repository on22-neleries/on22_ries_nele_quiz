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

//aktuelle Frage
const getCurrentQuestion = computed(() => {
	let question = questions.value[currentQuestion.value]
	question.index = currentQuestion.value
	return question
})

//Funktion zum Setzen der Antwort
const SetAnswer = (e) => {
	questions.value[currentQuestion.value].selected = e.target.value
	e.target.value = null
}

//Funktion für die nächste Frage
const NextQuestion = () => {
	if (currentQuestion.value < questions.value.length - 1) {
		currentQuestion.value++
		return
	}
	
	quizCompleted.value = true
}
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
  <main class="app">
		<h1>Das Nordsee-Quiz🌊</h1>
		
		<!--Quiz-Bereich-->
		<section class="quiz" v-if="!quizCompleted">
			<!--Fragenanzeige-->
			<div class="quiz-info">
				<span class="frage">{{ getCurrentQuestion.question }}</span>
			</div>

      <!--Punktestand-->
			<div class="punktestand">
				<span class="Punkt">Punkte {{ score }}/{{ questions.length }}</span>
			</div>

      <!--Antwortoptionen-->
			<div class="options">
				<label 
					v-for="(option, index) in getCurrentQuestion.options" 
					:for="'option' + index" 
					:class="`option ${
						getCurrentQuestion.selected == index 
							? index == getCurrentQuestion.answer 
								? 'richtig' 
								: 'falsch'
							: ''
					} ${
						getCurrentQuestion.selected != null &&
						index != getCurrentQuestion.selected
							? 'disabled'
							: ''
					}`">
					<input 
						type="radio" 
						:id="'option' + index" 
						:name="getCurrentQuestion.index" 
						:value="index" 
						v-model="getCurrentQuestion.selected" 
						:disabled="getCurrentQuestion.selected"
						@change="SetAnswer" 
					/>
					<span>{{ option }}</span>
				</label>
			</div>

    </section>

    <!--Button "Nächste Frage"-->
		<button 
				v-if="!quizCompleted"
				@click="NextQuestion" 
				:disabled="!getCurrentQuestion.selected"
				class="quiz-button">

				{{ 
					getCurrentQuestion.index == questions.length - 1 
						? 'Fertig' 
						: getCurrentQuestion.selected == null
							? 'Wähle die richtige Antwort aus'
							: 'Nächste Frage'
				}}
		</button>

    <!--Ergebnisanzeige-->
		<section v-else class="result-box">
			<h2>Du hast das Quiz beendet!</h2>
			<p>Deine Punktzahl: {{ score }}/{{ questions.length }}</p>
		</section>

    </main>
</template>


