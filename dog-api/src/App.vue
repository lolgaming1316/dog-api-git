<template>
  <title>Dog breeds</title>
  <AppHeader />
  <div class="wrapper">
    <div class="info">
      <h1 class="header-text">Dog Breeds</h1>
      <h2 class="header-text2">Dog Breeds</h2>
      <div class="select-border">
        <select class="select" v-model="selectedBreed">
          <option value="" disabled>Select a breed</option>
          <option v-for="(breed, index) in breeds" :key="index" :value="breed">
            {{ breed }}
          </option>
        </select>
      </div>
      <button
        class="fetch-button"
        @click="fetchBreedImage"
        :disabled="!selectedBreed"
      >
        Show Image
      </button>
    </div>
    <div v-if="error" class="error">{{ error }}</div>
    <div class="image-container" v-if="breedImage">
      <img class="breed-image" :src="breedImage" alt="Selected breed image" />
    </div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Home",
  data() {
    return {
      breeds: [],
      loading: true,
      error: null,
      selectedBreed: "",
      breedImage: null,
    };
  },
  methods: {
    fetchBreeds() {
      fetch("https://dog.ceo/api/breeds/list/all")
        .then((response) => {
          if (!response.ok) {
            throw new Error("Failed to fetch breeds");
          }
          return response.json();
        })
        .then((data) => {
          this.breeds = Object.keys(data.message);
          this.loading = false;
        })
        .catch((error) => {
          this.error = error.message;
          this.loading = false;
        });
    },
    fetchBreedImage() {
      if (!this.selectedBreed) return;
      this.loading = true;
      this.error = null;
      fetch(`https://dog.ceo/api/breed/${this.selectedBreed}/images/random`)
        .then((response) => {
          if (!response.ok) {
            throw new Error("Failed to fetch breed image");
          }
          return response.json();
        })
        .then((data) => {
          this.breedImage = data.message;
          this.loading = false;
        })
        .catch((error) => {
          this.error = error.message;
          this.loading = false;
        });
    },
  },
  created() {
    this.fetchBreeds();
  },
};
</script>

<style scoped>
.wrapper {
  width: 100vw;
  height: 100%;
  max-height: 100%;
  max-width: 100vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow: hidden;
  background-color: var(--background-purple);
}

/* Base styles (for mobile-first design) */
.wrapper {
  padding: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* Tablets and small desktops (min-width: 768px) */
@media (min-width: 768px) {
  .wrapper {
    max-width: 100%;
    margin: auto;
    flex-direction: column;
    justify-content: center;
  }

  .info {
    margin-top: 10%;
  }

  .image-container {
    margin-top: 20%;
    width: 50%;
  }

  .fetch-button {
    padding: 15px 25px;
    font-size: 1rem;
  }
}

/* Large desktops (min-width: 1280px) */
@media (min-width: 1280px) {
  .wrapper {
    max-width: 100vw;
    max-height: 100vh;
    flex-direction: row;
  }


  .fetch-button {
    padding: 20px 40px;
    font-size: 1.2rem;
  }

  .image-container {
    width: 100%;
    height: 100%;
    max-width: 100vw;
    max-height: 100vh;

  }
}

/* Ultra-wide screens (min-width: 1920px) */
@media (min-width: 1920px) {
  .wrapper {
    max-width: 100%;
    max-height: 100%;
    width: 100vw;
    display: flex;
    flex-direction: row;
    align-items: center;
    overflow: hidden;
  }

  .fetch-button {
    padding: 25px 50px;
    font-size: 1.5rem;
    margin-bottom: 0%;
  }

  .header-text {
    font-size: 4rem;
  }

  .header-text2 {
    font-size: 4rem;
  }

  .image-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 50%;
    width: 50%;
  }
}

.breeds-list {
  list-style: none;
  padding: 0;
  margin: 20px 0;
  text-align: center;
}

.breeds-list li {
  margin: 5px 0;
}

.header-text {
  color: var(--turquoise-green);
  font-size: calc(1px + 2rem);
  position: relative;
  z-index: 0;
  filter: blur(7px);
  opacity: 0.8;
  margin-bottom: 4%;
}

.header-text2 {
  color: var(--turquoise-green);
  position: absolute;
  z-index: 0;
  font-size: 2rem;
  margin-bottom: 4%;

}

.select {
  height: 150%;
  width: 100%;
  color: #ffffff;
  background: linear-gradient(90deg, #6d597a, #4a7c8e);
}

select option {
  color: black;
}

.select-border {
  border: 1px solid;
  border-image: linear-gradient(90deg, #6d597a, #4a7c8e) 1;
  margin-bottom: 4%;
}

.fetch-button {
  padding: 10px 20px;
  background-color: var(--turquoise-green);
  border: none;
  color: black;
  cursor: pointer;
}

.fetch-button:disabled {
  background-color: gray;
  cursor: not-allowed;
}

.image-container {
  margin-top: 0;
  height: 100%;
  width: 100%;
  max-width: 100vw;
  max-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow: hidden;
  background-color: var(--background-purple);
  padding: 10%;
}

.breed-image {
  max-width: 50vw;
  max-height: 50vh;
  object-fit: contain;
  border: solid;
  border-color: var(--turquoise-green);
  border-radius: 10px;
}

.info {
  margin-top: 7%;
  width: 100vw;
  padding: 2%;
  display: flex;
  flex-direction: column;
  align-items: center;

}
</style>
