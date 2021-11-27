<template>
    <div class="flex">
        <div class="gameCards" v-for="card in cardsDuplicated" :key="card.name">
            <img :src="card.path" :alt="card.name" @click="game(card)">  
        </div>
    </div>       
</template>

<script>
export default {
    props: ['cards'],
    // ********************************************
    // ********************************************
    data() {
        return {
            cardsDuplicated: [],
            counterPairFound: 0,
            counterTurns: 0,
            pairOfCards: []
        }
    },  
    // ********************************************
    // ********************************************
    mounted() {
        this.duplicateArray(),
        this.shuffleArray()
        this.frontToBackAllImg()
    },
    // ********************************************
    // ********************************************
    methods: {
        // ********************************************
        duplicateArray() 
        {
			for( let i=0 ; i<2 ; i++ )
			{
				for( let j=0 ; j<this.cards.length ; j++)
				{
					const newObject = {
						name: this.cards[j].name, 
						path: this.cards[j].path
					}
					this.cardsDuplicated.push(newObject)
				}
			}
		},
        // ********************************************
        shuffleArray() 
        {			
			for (let a = 0; a < this.cardsDuplicated.length; a++) {
				let x = this.cardsDuplicated[a];
				let y = Math.floor(Math.random() * (a + 1));
				this.cardsDuplicated[a] = this.cardsDuplicated[y];
				this.cardsDuplicated[y] = x;
            }
		},	
        // ********************************************
        frontToBackAllImg() 
        {			
            this.cardsDuplicated.forEach((card) => {
                card.path = "https://m.media-amazon.com/images/I/415bjCpaP8L._AC_SS450_.jpg"
            })
		},
        // ********************************************
        backToFrontImg(card) 
        {
            switch (card.name) {                
                case "Mario":
                    card.path = "https://i.pinimg.com/736x/3d/18/cb/3d18cb2fb0a76266cfa398c23b217d1c.jpg"
                    break;
                case "Bowser":
                    card.path = "https://i.pinimg.com/originals/48/5f/68/485f686c9eab124677dce0ca7192f60a.png"
                    break;
                case "Peach":
                    card.path = "https://e7.pngegg.com/pngimages/673/838/png-clipart-super-mario-bros-princess-peach-super-paper-mario-mario-princess-super-mario-bros-video-game.png"
                    break;
                case "Yoshi":
                    card.path = "https://e7.pngegg.com/pngimages/919/555/png-clipart-super-mario-yoshi-mario-yoshi-super-mario-world-2-yoshi-s-island-paper-mario-the-thousand-year-door-paper-mario-sticker-star-yoshi-leaf-nintendo.png"
                    break;
                case "Luigi":
                    card.path = "https://e7.pngegg.com/pngimages/612/233/png-clipart-mario-luigi-paper-jam-mario-luigi-superstar-saga-luigi-s-mansion-luigi.png"
                    break;
                default:
                    break;
            }
        },
        // ********************************************
        checkPairOfCards(pairOfCards) 
        {
			
			// check cards'names and positions
			if( (pairOfCards[0] === pairOfCards[2]) && (pairOfCards[1] != pairOfCards[3]) )
			{
				this.counterPairFound++ 
                this.$emit('paire', this.counterPairFound)

                const arrayPairOfCards = document.querySelectorAll("img[alt=" + pairOfCards[0] + "]")
                arrayPairOfCards.forEach(function(item){
                    item.classList.add("isFind")
                })

                
			}

            // reset board
            setTimeout (() => {
                this.pairOfCards = []   
                this.frontToBackAllImg()
                this.toggleImagesClickEvent()
            }, 700)

            
		},
        // ********************************************
        toggleImagesClickEvent() 
        {			
            const images = document.querySelectorAll("img")
            images.forEach(function(image){
                image.classList.toggle("activeImage")
            })
		},
        // ********************************************
        game(card)
        {
            this.backToFrontImg(card)
            this.pairOfCards.push(card.name)
			this.pairOfCards.push(this.cardsDuplicated.indexOf(card))

            if(this.pairOfCards.length >= 4)
            {
                this.toggleImagesClickEvent()
                this.checkPairOfCards(this.pairOfCards)
                this.counterTurns++
                this.$emit('turn', this.counterTurns)
            }
        }
    }
}
</script>

<style>
    .gameCards img {
        height: 150px;
        width: 150px;
        margin: 15px;
        border-radius: 10px;
        cursor: pointer;
    }
    .isFind {
        opacity: 0;
        transition-property: opacity;
        transition-timing-function: ease-in-out;
        transition-duration: 1s;
        pointer-events: none;
    }
    .activeImage {
        pointer-events: none;
    }
</style>