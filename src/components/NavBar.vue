<script>
export default {
  data() {
    return {}
  }
}
</script>

<template>
  <nav id="navbar">
    <div id="navbar-container">
      <h1>Vendre</h1>
      <p>by optimizers</p>
    </div>
  </nav>
</template>

<style scoped>
#navbar {
  background-color: rgb(255, 255, 255);
  position: relative;
  z-index: 1;
  display: flex;
  align-items: center;
  top: 0;
  width: 100%;
}

#navbar-container {
  margin: 15px auto 15px 25px;
  text-align: right;
}

#navbar-container h1 {
  margin: 0;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial,
    sans-serif;
  font-size: 2.5rem;
}

#navbar-container p {
  margin: 0;
  font-size: 1rem;
}
</style>
