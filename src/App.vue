<template>

	<div class="title-container">
		<h1>Memory Paper Mario</h1>
	</div>

	<!-- start game -->
	<button @click="startGame" ><i class="far fa-play-circle"></i></button>


	<EndGame v-if="endGame" />	
  	<Results v-if="isPlaying" :turn="turn" :paire="paire" />
    <Block v-if="isPlaying" :cards="cards" @turn="showCounterTurns" @paire="showCounterPaireFound" />
</template>

<script>
import Block from './components/Block'
import Results from './components/Results'
import EndGame from './components/EndGame'

export default {
  	name: 'App',
	components: { Block, Results, EndGame },
	data() {
		return {
		isPlaying: false,
		endGame: false,
		turn: 0,
		paire: 0,
		cards: [ 
			{ 
				name: "Mario", 
				path:"https://i.pinimg.com/736x/3d/18/cb/3d18cb2fb0a76266cfa398c23b217d1c.jpg"
			}, 
			{ 
				name: "Bowser", 		
				path:"https://i.pinimg.com/originals/48/5f/68/485f686c9eab124677dce0ca7192f60a.png"
			},
			{ 	
				name: "Peach", 
				path:"https://e7.pngegg.com/pngimages/673/838/png-clipart-super-mario-bros-princess-peach-super-paper-mario-mario-princess-super-mario-bros-video-game.png"
			},
			{
				name: "Yoshi",
				path: "https://e7.pngegg.com/pngimages/919/555/png-clipart-super-mario-yoshi-mario-yoshi-super-mario-world-2-yoshi-s-island-paper-mario-the-thousand-year-door-paper-mario-sticker-star-yoshi-leaf-nintendo.png"
			},
			{
				name: "Luigi",
				path: "https://e7.pngegg.com/pngimages/612/233/png-clipart-mario-luigi-paper-jam-mario-luigi-superstar-saga-luigi-s-mansion-luigi.png"
			}
		]
		}
	},
	methods: {
		startGame() {
			this.isPlaying = true
			document.querySelector('button').style.display = "none"
		},
		showCounterTurns(counterTurns) {
			this.turn = counterTurns
		}, 
		showCounterPaireFound(counterPairFound) {

			// endgame ?
			if(counterPairFound === 5) {
				this.isPlaying = false
				this.endGame = true
			}

			this.paire = counterPairFound
		}
	}
	}
	</script>

	<style>
	body {
		color: black;
		background-image: url('./assets/bgc_paper_mario.jpg');
		background-repeat: no-repeat;
		background-size: cover;
	}
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		margin: 0 auto;
		max-width: 1000px;
	}
	.flex {
		display: flex;
		flex-direction: row;
		justify-content: center;
		text-align: center;
		flex-wrap: wrap;
	}
	.title-container {
		margin: 0 auto;
		width: 80%;
		border-radius: 10px;	
		background-color: rgba(255, 255, 255, .9);
	}
	h1 {
		padding: 15px 0;
		margin-top: 10%;
		font-weight: bold;
		font-size: 4rem;
		color:#B70714;
	}
	button {
		padding: 100px;
		border-radius: 15px;
		border: .7rem #F7AE11 solid;
	}
	button:hover {
		border: .7rem #B70714 solid;
	}
	.fa-play-circle {
		font-size: 18rem;
		color: #333;
	}
</style>