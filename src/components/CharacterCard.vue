<template>
  <div class="character">
    <div class="character__card">
      <img class="character__img" :src="character.image">
      <div class="character__info">
        <div class="character__name">
          {{ character.name }}
        </div>
        <div class="character__status">
          <span
            :style="[character.status !== 'unknown' ? character.status === 'Alive' ? {'background': 'green'} : {'background': 'red'} : {'background': 'grey'}]"
            class="status-icon"/> {{ character.status }}
        </div>
        <div class="character__sex">
          {{ character.gender }}
        </div>
        <div class="character__location">
          {{ character.location.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CharacterCard",
  data() {
    return {
      query: `https://rickandmortyapi.com/api/character/${this.$route.params.character}`,
      character: {
        name: String,
        image: String,
        gender: String,
        location: Object,
        status: String
      },
      location: ''
    }
  },
  methods: {
    async fetchData() {
      const r = await fetch(this.query)
      const {name, image, gender, location, status} = await r.json()
      this.character = {name, image, gender, location, status}
    },
  },
  mounted() {
    this.fetchData();
  }
}
</script>

<style scoped lang="scss">
.character {
  padding: 2rem;
  background-color: #434343;
  min-height: 100vh;

  &__card {
    display: flex;
    justify-content: space-between;
  }

  &__img {
    height: 100%;
    object-fit: contain;
    display: block;
    max-width: 49%;
    width: 100%;
    flex-basis: 49%;
  }

  &__info {
    flex-basis: 49%;
    color: white;

    & > div {
      margin-bottom: 1rem;
    }

    & > div:last-child {
      margin-bottom: 0;
    }
  }

  &__name {
    text-align: center;
    font-size: 80px;
  }

  &__status {
    display: flex;
    align-items: center;
    font-size: 25px;
  }

  &__sex {
    font-size: 25px;
  }

  &__location {
    font-size: 30px;
  }

  .status-icon {
    display: block;
    margin-right: 10px;
    width: 0.5rem;
    height: 0.5rem;
    border-radius: 50%;
  }
}

@media screen and(max-width: 1137px) {
  .character {
    &__card {
      display: block;
    }

    &__img {
      width: 100%;
      max-width: 100%;
      display: block;
    }

    &__info {
      margin-top: 25px;
    }

    &__name {
      font-size: 30px;
    }
  }
}

@media screen and(max-width: 500px) {
  .character {
    padding: 0;

    &__info {
      padding: 15px;
      margin-top: 0;
    }
  }
}
</style>
