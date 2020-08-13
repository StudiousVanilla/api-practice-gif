<template>
  <div id="container">
    <div id="gif-container">
      <img id="gif" v-bind:src="imgSRC" alt />
    </div>
    <div id="search-container">
      <!-- Whatever the user inputs is bound to the variable 'searchTerm'-->
      <input
        class="search"
        type="text"
        placeholder="cats..."
        v-model="searchTerm"
      />
      <!-- Once the button is clicked, the showGif function fetchs data from the giphy api with the 's' (search term) request parameter set to eqaul the 'searchTerm' variable-->
      <button class="btn" v-on:click="showGif(searchTerm)">Gif Me!</button>
    </div>
    <p>{{ errorMessage }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // this variable will be passed to 'showGif' when the button is pressed, altering the URL to whatever is searched for
      searchTerm: "",
      imgSRC: "",
      errorMessage: ""
    };
  },
  methods: {
    // 'x' will be the searchTerm variable set by the two way data binding of search input
    async showGif(x) {
      let img = document.querySelector("#gif");
      try {
        // get response promise from API using 'await' key word
        const response = await fetch(
          "https://api.giphy.com/v1/gifs/translate?api_key=Cv2mbWyZIxZz5EKVfbVyw1rYLSrZuJew&s=" +
            x,
          { mode: "cors" }
        );
        // set catData to equal the response promise that has been parsed into an object, again using 'await'
        const catData = await response.json();

        // once promise has been resolved, set 'img.src' to the relevant data from the 'catData' object
        this.imgSRC = await catData.data.images.original.url;
        this.errorMessage = "";

        // Log errors when caught, and show a 'nope' gif to users
      } catch (error) {
        this.errorMessage = "Netowrk is slow, keep trying!";
        console.log(error);
      }
    }
  },

  // add an on 'created' function that calls showGif with the 'cat' parameter as a placeholder for  when the page first loads
  mounted() {
    this.showGif("cat");
  }
};
</script>

<style scoped>
#container {
  height: 80%;
  width: 100%;
  margin: 6% 0 0 0;

  display: flex;
  justify-content: space-evenly;
  align-items: center;

  flex-direction: column;
}

#gif-container {
  width: 50%;
  height: 80%;
  background-color: white;
}

#search-container {
  height: 20%;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
}

.search {
  width: 50vw;
  height: 4vh;
  background-color: rgb(216, 208, 208);
  border: none;
  font-size: 3vh;
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
}

.btn {
  width: 15vw;
  height: 6vh;
  font-size: 3vh;
  background-color: rgb(10, 214, 10);
  border: none;
  color: white;
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
}

::-webkit-input-placeholder {
  font-style: italic;
}
:-moz-placeholder {
  font-style: italic;
}
::-moz-placeholder {
  font-style: italic;
}
:-ms-input-placeholder {
  font-style: italic;
}

img {
  width: 100%;
  height: 100%;
}

@media only screen and (max-width: 860px) {
  #gif-container,
  #search-container {
    width: 75%;
  }

  .search {
    width: 100%;
  }

  .btn {
    width: 50%;
  }
}

@media only screen and (max-width: 1100px) {
  #gif-container,
  #search-container {
    width: 70%;
  }

  .search {
    width: 100%;
  }

  .btn {
    width: 50%;
  }
}
</style>

<!--  Add an error message in the catch chain-->
