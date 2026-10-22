<script lang="js" setup>
defineProps({
  avatar: {
    type: Object,
    default: () => ({
      name: { type: String, required: true },
      img: { type: String, required: true },
      text: { type: String, required: true },
    }),
  },
});
</script>
<template>
  <div class="avatar-inner">
    <img :src="avatar.img" class="img" />
    <div>
      <p class="avatar-name">{{ avatar.name }}</p>
      <p class="avatar-text">{{ avatar.text }}</p>
    </div>
  </div>
</template>
<style scoped>
html,
body {
  margin: 0;
  padding: 0;
  font-family: 'Roboto', sans-serif;
}

/* typography and icons */

h1 {
  color: #0f8cdf;
  margin-bottom: 10px;
  font-size: 20px;
}

i {
  font-size: 15px;
  cursor: pointer;
}

.fa-solid {
  color: #999;
}

.liked {
  color: red;
}

.retweeted {
  color: limegreen;
}

/* layout */

main,
header {
  width: 290px;
  margin: 0 auto;
}

header {
  padding-bottom: 25px;
}

textarea {
  border: none;
  resize: none;
  padding: 10px;
  margin: 0 0 20px 0;
  height: 60px;
  width: 100%;
  font-size: 20px;
  line-height: 30px;
}

button {
  background-color: #1da1f2;
  border: none;
  color: white;
  padding: 10px 19px;
  border-radius: 20px;
  width: 100%;
  cursor: pointer;
  font-size: 20px;
  font-weight: 600;
}

.avatar {
  border-top: 1px solid lightgray;
  padding: 20px 0 0 0;
  width: 100%;
  margin: 15px 0;
}

.avatar-inner {
  display: flex;
  align-items: center;
  gap: 10px;
}

.avatar-details {
  display: flex;
  font-size: 13px;
  justify-content: space-between;
  width: 160px;
}

.avatar-detail {
  display: flex;
  gap: 4px;
}

.avatar-reply {
  border-top: 1px solid lightgray;
  padding: 20px 0 0 0px;
  margin: 10px 0 10px 40px;
  width: 80%;
}

.avatar-name {
  font-size: 12px;
  font-weight: 500;
  color: #555;
  margin-top: 0;
}

.avatar-text {
  width: 207px;
  font-size: 14px;
  line-height: 20px;
}

/* images */

.img {
  border: 1px solid lightgray;
  border-radius: 50%;
  width: 60px;
  height: 60px;
  object-fit: cover;
  text-align: center;
}

/* utility */
.hidden {
  display: none;
}
</style>
