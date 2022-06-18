<template>
  <header>
    <h1>ADM</h1>
    <nav>
      <ul>
        <li>
          <router-link to="/kanban"
            ><ion-icon name="card-outline"></ion-icon> Kanban</router-link
          >
        </li>
        <li>
          <router-link to="/dtd"
            ><ion-icon name="stopwatch-outline"></ion-icon> DTD</router-link
          >
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  name: "MainHeader",
};
</script>

<style scoped>
header {
  background-color: cornflowerblue;
  color: white;
  text-align: center;
}

header h1 {
  padding: 2%;
}

nav {
  background-color: #5881cc;
  padding: 2%;
}

nav a {
  color: white;
}

ul {
  list-style: none;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
</style>