<template>
  <div class="card_container">
    <img :src="anime.attributes.posterImage.small" alt="" class="card_img" />
    <div class="card_info">
      <div class="txt_info">
        <h2 class="card_title">
          {{ anime.attributes.titles.en_jp }}
        </h2>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["anime"],
};
</script>

<style>
.card_container {
  width: 284px;
  height: 402px;
  margin-right: 1em;
  margin-bottom: 1em;
  position: relative;
}
.card_title {
  font-size: 1.2em;
  font-weight: 500;

  margin: 0;
}
.card_img {
  width: 284px;
  height: 402px;
}
.txt_info {
  padding: 1em;
}
.card_info {
  position: absolute;
  bottom: 0;
  background: rgba(0, 0, 0, 0.733);
  width: 100%;
}
</style>
