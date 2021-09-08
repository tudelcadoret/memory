<template>
  <h1>Memory Paper Mario</h1>
  <button @click="start" :disabled="isPlaying">play</button>


  <div class="flex">
    <Block :delay="delay" :cards="cards" @turn="showCounterTurns" @paire="showCounterPaireFound" />
    <Results v-if="showResults" :score="score" :turn="turn" :paire="paire" />
  </div>
  
</template>

<script>
import Block from './components/Block'
import Results from './components/Results'
export default {
  name: 'App',
  components: { Block, Results },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: true,
      test: null,
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
				}
			]
    }
  },
  methods: {
    // start() {
    //   // set time amount (ms)
    //   this.delay = 2000 + Math.random() * 1000
    //   this.isPlaying = true
    //   this.showResults = false
    // }, 
    showCounterTurns(counterTurns) {
      this.turn = counterTurns
    }, 
    showCounterPaireFound(counterPairFound) {
      this.paire = counterPairFound
    }
    // endGame(reactionTime) {
    //   this.score = reactionTime
    //   this.isPlaying = false
    //   this.showResults = true
    // }
  }
}
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: white;
    background-image: url('./assets/bgc_paper_mario.jpg');

  }
  .flex {
    display: flex;
    flex-direction: row;
    justify-content: center;
    text-align: center;
  }
  button {
    background: #0faf87;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    font-size: 16px;
    letter-spacing: 1px;
    cursor: pointer;
    margin: 10px;
  }
  button[disabled] {
    opacity: 0.2;
    cursor: not-allowed;
  }
  section {
        margin: 10px;
        background-color: lightgray;
        border-radius: 20px;
  }
  #app section:nth-child(1) {
    flex: 3;
  }
  #app section:nth-child(2) {
    flex: 1;
  }
</style>