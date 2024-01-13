<template>
    <div id="form" class="center">
      <div v-for="word in words" :key="word.id" class="word">
        <div v-for="letter in word.letters" :key="letter.id" class="letter">
          <input
            type="text"
            v-model="letter.value"
            maxLength="1"
            size="1"
            pattern="[a-zA-Z]{1}"
          />
        </div>
        <div class="horizontal-blank-space"></div> <!-- Horizontal blank space at the end of each word -->
      </div>
      
      <div>
        <button class="btn btn-primary btn-embossed">Verify</button>
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
    }
  };
  </script>
  
  <style scoped>
  .center {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .word {
    display: flex;
    align-items: center;
    margin-right: 10px;
  }
  
  .letter {
    margin-right: 5px; /* Adjust the margin between letters as needed */
  }
  
  .horizontal-blank-space {
    width: 10px; /* Adjust the width of the blank space at the end of each word */
  }
  </style>
  