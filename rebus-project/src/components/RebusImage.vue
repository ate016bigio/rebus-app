<!-- RebusImage.vue -->

<template>
    <div>
      <h2 class="hint-heading">Hint: {{ hint }}</h2>
      <img :src="imageSrc" class="responsive-image" />
    </div>
  </template>
  
  <script>
  export default {
    props: {
      imageSrc: {
        type: String,
        required: true,
      },
      hint: {
        type: String,
        required: true,
      }
    },
  };
  </script>
  
  <style scoped>
  .responsive-image {
    max-width: min(100%, 600px);
    height: auto;
    display: block;
    margin: 0 auto;
  }

  .hint-heading {
  font-size: 1.5em; /* Adjust the font size as needed */
  color: #333; /* Adjust the color as needed */
  margin-bottom: 10px;
  margin-top: 60px;
}
  </style>
  