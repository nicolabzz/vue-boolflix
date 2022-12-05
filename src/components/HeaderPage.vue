<template>
  <header>
    <nav>
      <h1>BOOLFLIX</h1>
      <span>
        <input
          @change="$emit('getSearchQuery', userInput)"
          @keydown.enter="$emit('getSearchQuery', userInput)"
          v-model="userInput"
          type="text"
          id="searchBar"
          placeholder="search"
        />
      </span>
    </nav>
  </header>
</template>

<script>
export default {
  name: "HeaderPage",
  data() {
    return {
      userInput: "",
    };
  },
};
</script>

<style lang="scss">
@import "../styles/general.scss";

header {
  width: 100%;
  z-index: 90;
  position: fixed;
  top: 0;
  overflow: hidden;
  padding: 20px 0;
  background-color: black;

  nav {
    width: 80%;
    margin: auto;
    display: flex;
    justify-content: space-between;
    align-items: center;

    h1 {
      font-size: 2.2rem;
      color: #e50914;
    }

    input {
      background-color: rgb(60, 61, 60);
      filter: brightness(3);
      padding: 5px 20px;
      border-radius: 3px;
    }
  }
}
</style>
