<template>
    <header class="app-header">
      <div class="left">
        <h1 class="header-text">Dog API</h1>
        <h1 class="header-text2">Dog API</h1>
        <nav>
          <ul v-if="LoggedIn"></ul>
        </nav>
      </div>
      <nav class="right">
      </nav>
    </header>
  </template>
  
  <script>
  
    export default {
      name: 'AppHeader',
    };
  </script>
  
  <style scoped>
    .app-header {
    background-color: var(--header-color);
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 1000;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem;
    box-sizing: border-box;
  }
  
  
  .app-header::before {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 4px;
    background: linear-gradient(to right, #FF77E9, #00F5D4);
  }
  
  
  .header-text {
    color: var(--neon-pink);
    position: relative;
    z-index: 2;
    font-size: 2rem;
  }
  
  .header-text2 {
    color: var(--neon-pink);
    font-size: calc(1px + 2rem);
    position: absolute;
    top: 0;
    left: -3px;
    z-index: 1;
    filter: blur(3px);
    opacity: 0.8;
  }
  
  .left {
    position: relative;
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  
    nav ul {
      list-style: none;
      display: flex;
      gap: 1rem;
    }
  
    nav a, .logout-link {
      color: white;
      text-decoration: none;
      cursor: pointer;
    }
  
    .right {
      margin-left: auto;
    }
  
    body {
    margin: 0;
    padding: 0;
    padding-top: 5rem; /* Adds space for fixed header */
  }
  </style>
  