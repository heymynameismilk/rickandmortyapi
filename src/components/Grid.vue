<template>
  <div class="grid">
    <ProfileCard v-for="profile in profiles" :profile="profile" :key='profile.id'/>
  </div>
</template>

<script>
import ProfileCard from './ProfileCard.vue'

export default {
  name: 'Grid',
  components: {
    ProfileCard
  },
  data() {
    return {
      profiles: [],
      nextQuery: '',
      firstQuery: 'https://rickandmortyapi.com/api/character/'
    }
  },
  methods: {
    async fetchData() {
      let r = await fetch(this.firstQuery)
      const data = await r.json()
      this.profiles = data.results
      this.nextQuery = data.info.next
    },
    async fetchMore() {
      let r = await fetch(this.nextQuery)
      const data = await r.json()
      this.profiles = this.profiles.concat(data.results)
      this.nextQuery = data.info.next
    },
    scroll(){
      window.onscroll = () => {
        let bottom = document.documentElement.scrollTop + window.innerHeight === document.documentElement.offsetHeight;
        if (bottom && this.nextQuery !== null) {
            this.fetchMore();
        }
      }
    }
  },
  mounted() {
    this.fetchData(this.firstQuery);
    this.scroll();
  },
}
</script>

<style lang="scss" scoped>
.grid {
  background-color: #434343;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-column-gap: 2rem;
  grid-row-gap: 2rem;
  padding: 1rem;
}

@media screen and(max-width: 1137px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
}


@media screen and(max-width: 760px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and(max-width: 490px) {
  .grid {
    grid-template-columns: repeat(1, 1fr);
  }
}

</style>
