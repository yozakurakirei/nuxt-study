<template>
  <div class="hero">
    <img src="../assets/image/iradesign1.png" alt="トップ画像" height="400px" width="1000px">
    <div class="text-container">
      <div class="text">
        <span class="mini-heading">Now Starting!</span>
        <h1><span>さぁ、</span>開発環境を<br>調べてみよう!</h1>
        <a href="#movie-grid" class="button"></a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "hero",
}
</script>
<style lang="scss" scoped>
.hero {
  height: 400px;
  position: relative;
  @media (min-width: 750px) {
    height: 500px;
  }

  &::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    background-color: rgba(0,0,0, .6);
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .text-container {
    z-index: 10;
    position: absolute;
    top: 5rem;
    margin: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;

    .text {
      padding: 0 16px;
      width: 100%;
      max-width: 1400px;
      margin: 0 auto;
    }
    
    .mini-heading {
      font-weight: bold;
      font-size: 1.8rem;
      color: #444;
      margin-bottom: .8rem;

      @media (min-width: 750px) {
        font-size: 2rem;
      }

    }
    h1 {
      color: #fefefe;

      span {
        font-weight: bold;
        color: aquamarine;
      }
    }
  }
}



</style>
