<script setup>
import { ref } from "vue";

// [ my states]  //

// state for conditionally showing model//
const showModel = ref(false);
// state for storing the textarea in model//
const noteTextarea = ref("");
// Note stete as array //
const notes = ref([]);
// Erroq  message //
const errorMessage = ref("");

// function to generate random color //
function getRandomColor() {
	return "hsl(" + Math.random() * 360 + ",  100%, 75%)";
}

// Add note handle thats push notes to an array //
const addNote = () => {
	// validating the textarea //
	if (noteTextarea.value.length < 6) {
		return (errorMessage.value =
			"Notes to be more than 10 characters or more ");
	}
	notes.value.push({
		id: Math.floor(Math.random() * 1000000),
		text: noteTextarea.value,
		date: new Date(),
		color: getRandomColor(),
	});

	// reseting some state //
	showModel.value = false;
	noteTextarea.value = "";
	errorMessages.value = "";
};
</script>

<template>
	<main>
		<div v-if="showModel" class="overlay">
			<div class="model">
				<textarea
					v-model.trim="noteTextarea"
					name="note"
					id="note"
					cols="30"
					rows="10"
				></textarea>
				<p v-show="errorMessage">{{ errorMessage }}</p>
				<button @click="addNote">Add Note</button>
				<button @click="showModel = false" class="close">close</button>
			</div>
		</div>
		<div class="container">
			<header>
				<h1>Note</h1>
				<button @click="showModel = true">+</button>
			</header>
			<div class="card-container">
				<div
					v-for="note in notes"
					class="card"
					:style="{ backgroundColor: note.color }"
					:key="note.id"
				>
					<p class="main-text">{{ note.text }}</p>
					<p class="date">
						{{ note.date.toLocaleDateString("en-US") }}
					</p>
				</div>
			</div>
		</div>
	</main>
</template>

<style scoped>
main {
	height: 100vh;
	width: 100vw;
}

.container {
	max-width: 1000px;
	padding: 10px;
	margin: 0 auto;
}

header {
	display: flex;
	justify-content: space-between;
	align-items: center;
}

h1 {
	font-weight: bold;
	margin-bottom: 25px;
	font-size: 75px;
}

header button {
	border: none;
	padding: 10px;
	width: 50px;
	height: 50px;
	cursor: pointer;
	background-color: rgb(21, 20, 20);
	border-radius: 100%;
	color: white;
	font-size: 20px;
}

.card {
	width: 225px;
	hight: 225px;
	background-color: rgb(237, 184, 44);
	padding: 10px;
	border-radius: 15px;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	margin-right: 20px;
	margin-bottom: 20px;
}

.date {
	font-size: 12.5px;
	font-weight: bold;
}

.card-container {
	display: flex;
	flex-wrap: wrap;
}

.overlay {
	position: absolute;
	width: 100%;
	height: 100%;
	background-color: rgba(0, 0, 0, 0.77);
	z-index: 10;
	display: flex;
	align-items: center;
	justify-content: center;
}

.model {
	width: 750px;
	background-color: white;
	border-radius: 10px;
	padding: 10px;
	display: flex;
	flex-direction: column;
}

.model button {
	padding: 10px 20px;
	font-size: 20px;
	widows: 100%;
	background-color: blueviolet;
	border: none;
	color: white;
	cursor: pointer;
	margin-top: 15px;
}

.model .close {
	background-color: rgb(176, 4, 4);
	margin-top: 7px;
}
.model p {
	color: red;
}
</style>
