<template>
  <header>
    <router-link to="/">
      <!-- <div class="logo">
        <img src="../assets/shopifyLogo.png" alt="" />
        <h1><span>The </span>Shoppies</h1>
      </div> -->
    </router-link>
  </header>
</template>

<script>
export default {
  data() {
    return {
      //   menu: ["Home", "About", "Gallery", "Contect"],
    };
  },
};
</script>

<style scoped>
header {
  display: flex;
  align-items: center;
  padding: 10px 16px;
  background-color: #2c3d4e;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);
  /* margin-bottom: 20px; */
}

h1 {
  color: #fff;
  font-size: 28px;
}

span {
  color: #42bbb3;
}
.logo {
  display: flex;
  justify-content: center;
  align-items: center;
}
.logo img {
  width: 75px;
}
</style>
