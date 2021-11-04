<template>
  <div class="modal-overlay">
    <div class="modal">
        <img height="60" src="../assets/pokeball-png.png">
      <p>PLEASE WAIT, THE POKÉMON ARE LOADING ... </p>
    </div>
  </div>
</template>

<script>
  export default {
}
</script>

<style scoped>

.modal-overlay {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  background-color: #000000da;
}

.modal {
  text-align: center;
  background-color: #607597;
  height: 200px;
  width: 500px;
  margin-top: 10%;
  padding: 60px 0;
  border-radius: 20px;
}


p {
  font-size: 16px;
  margin: 20px 0;
}

</style>
