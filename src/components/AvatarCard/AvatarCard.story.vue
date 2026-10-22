<script setup>
  import AvatarCard from './AvatarCard.vue'
</script>
<template>
  <Story title="Components/AvatarCard">
    <Variant title="Default">
      <AvatarCard
      :avatar="{
        name: 'John Doe',
        img: 'https://randomuser.me/api/portraits/men/1.jpg',
        text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut'
      }"
      />
    </Variant>
  </Story>
  </template>
