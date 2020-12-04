<template>
  <NuxtLink :to="`/${profile.id}`">
    <div class="card">
      <img class="card__img" :src='profile.image'/>
      <div class="card__name">{{ profile.name }}</div>
    </div>
  </NuxtLink>
</template>

<script>

export default {
  name: "ProfileCard",
  props: ['profile'],
}
</script>

<style lang="scss" scoped>

.card {
  height: 100%;
  cursor: pointer;
  overflow: hidden;
  background-color: #343434;
  color: white;
  border-radius: 8px;
  box-shadow: 4px 4px 16px #262626,
  -4px -4px 16px #262626;
  transition: transform 0.13s ease-in-out;

  &:hover {
    transform: scale(1.05);
  }

  &__name {
    padding: 5px 10px;
    font-size: 30px;
    letter-spacing: 2px;
    text-align: center;
    justify-content: center;
    display: flex;
    align-items: center;
    height: calc(100% - 250px);
    word-break: break-word;
  }

  &__img {
    width: 100%;
    max-width: 100%;
    display: block;
    height: 250px;
    object-fit: cover;
    object-position: center;
  }
}
</style>
