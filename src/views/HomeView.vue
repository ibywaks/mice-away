<script setup lang="ts">
</script>

<template>
  <main>
    <div class="row">
      <div class="col-md-12 text-center mb-3">
        <span @click="selectTag(tag)" v-for="(tag, index) in visibileTags" :key="index" 
          class="badge rounded-pill fs-5 me-2" :class="[tag === activeTag ? 'text-bg-primary' : 'text-bg-secondary']">
            #{{tag}}
        </span>
        <span @click="showNext()" class="badge rounded-pill text-bg-light fs-4">...</span>
      </div>
    </div>
    <div v-if="catImage" class="row">
      <div class="col-md-12 text-center">
        <img :src="catImage" class="img-fluid" height="500" width="450" :alt="activeTag ?? 'Default image'">
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import type {AxiosInstance} from 'axios'

// declare module '@vue/runtime-core' {
//   interface ComponentCustomProperties {
//     $axios: AxiosInstance
//     catTags: string[]
//   }
// }

interface DogBreed {
  name: string
}

export default defineComponent({
  name: 'HomeView',
  data() {
    return {
      catTags: [] as string[],
      displayStart: 0,
      displayCount: 5,
      activeTag: '',
      catImage: '',
    };
  },
  computed: {
    cleanCatTags() {
      return this.catTags.filter((tag) => tag !== '').map((tag) => tag.replace(/[&\/\\#,+()$~%.'":*?<>{}]/g, ''))
    },
    totalTags() {
      return this.cleanCatTags.length
    },
    displayEnd() {
      const sliceEnd = this.displayCount + this.displayStart
      return this.totalTags > sliceEnd ? sliceEnd : this.totalTags
    },
    visibileTags() {
      return this.cleanCatTags.slice(this.displayStart, this.displayEnd)
    },
    hasNextTags() {
      return this.displayEnd < this.totalTags
    }
  },
  methods: {
    async fetchCatTags() {
      const tagsResponse = await this.$axios.get('/api/tags')
      this.catTags = tagsResponse.data
    },
    showNext() {
      this.displayStart += this.displayCount
      this.selectTag(this.cleanCatTags[this.displayStart])
    },
    selectTag(tag: string) {
      const baseUrl = 'https://cataas.com/'
      this.catImage = `${baseUrl}cat/${tag}`
      this.activeTag = tag
    },
    loadDefaultCatImage() {
      const baseUrl = 'https://cataas.com/'
      this.catImage = `${baseUrl}cat/gif`
    }
  },
  async mounted() {
    await this.fetchCatTags()
    this.loadDefaultCatImage()
  },
});
</script>
