<template>
    <div>
        <div id="form" class="center">
            <div v-for="word in words" :key="word.id" class="word">
                <div v-for="(letter, index) in word.letters" :key="index" class="letter">
                    <input
                        :id="'input_' + letter.id"
                        ref="inputField"
                        type="text"
                        v-model="letter.value"
                        maxLength="1"
                        size="1"
                        @keydown="onKeyDown"
                        @keyup="goToNextInput"
                        @click="onFocus"
                    />
                </div>
            </div>
            <div class="horizontal-blank-space"></div> <!-- Horizontal blank space at the end of each word -->
            <div>
                <button class="btn btn-primary btn-embossed verify-button" @click="verifySolution">Verify</button>
            </div>
        </div>

        <div class="solution-response" v-show="isSolutionGiven">
            <div class="solution-correct" v-if="isSolutionCorrect">
                <p>Solution correct!</p>
            </div>
            <div class="solution-correct" v-if="!isSolutionCorrect">
                <p>Solution wrong D:</p>
            </div>
        </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
        words: {
            type: Array,
            required: true,
        }
    },
    methods: {
        goToNextInput(event) {
            const key = event.which;
            const target = event.target;
            const currentId = parseInt(target.id.split('_')[1]);
            const nextInput = document.getElementById(`input_${currentId + 1}`);

            // Move forward if a letter is detected
            if (key !== 9 && !((key >= 65 && key <= 90) || (key >= 97 && key <= 122))) {
                event.preventDefault();
                return false;
            }

            // If tab, do not do anything
            if (key === 9) {
                return true;
            }

            target.value = event.key;
            this.solutionGiven += target.value;
            
            if (nextInput) {
                nextInput.focus();
            } else {
                const inputFields = this.$refs.inputField;
                const index = inputFields.indexOf(target);

                if (index !== -1 && inputFields[index + 1]) {
                inputFields[index + 1].select();
                inputFields[index + 1].focus();
                }
            }
        },

        onKeyDown(event) {
            const key = event.which;
            event.preventDefault();
            return false;
        },

        onFocus(event) {
            event.target.select();
        },

        verifySolution(){
            console.log(this.solutionGiven)
            this.isSolutionGiven = true
            if (this.solutionGiven.toLowerCase() === this.actualSolution) {
                console.log('Correct Solution')
                this.isSolutionCorrect = true
            } else {
                console.log('Wrong Solution')
                this.isSolutionCorrect = false
            }
            this.solutionGiven = ''
        }
    },
    data() {
        return {
            solutionGiven: '',
            actualSolution: 'ordadibarbari',
            isSolutionGiven: false,
            isSolutionCorrect: false,
        }
    }
  };
  </script>
  
<style scoped>
    #form {
        max-width: min(240px, 80%);
        margin: 25px auto 0;
    }¨
  
    #form input {
        margin: 5px;
        text-align: center;
        line-height: 80px;
        font-size: 50px;
        border: solid 1px #ccc;
        box-shadow: 0 0 5px #ccc inset;
        outline: none;
        width: 20%;
        transition: all .2s ease-in-out;
        border-radius: 3px;
    }

    #form input:focus {
        border-color: purple;
        box-shadow: 0 0 5px purple inset;
    }

    #form input::selection {
        background: transparent;
    }

    .center {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
        flex-direction: column;
    }
    
    .word {
        display: flex;
        align-items: center;
        margin-right: 10px;
        margin-bottom: 10px;
    }
    
    .letter {
        margin: 0 3px;
    }
    
    .horizontal-blank-space {
        width: 10px; /* Adjust the width of the blank space at the end of each word */
    }

    .verify-button {
        margin-top: 10px;  /* Margin between words and the button */
    }
</style>
  