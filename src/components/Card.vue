<template>
  <div class="card" @click="openWebsite(data.url)" :class="{ now: data.isNow }">
    <div class="name">
      {{ data.name }}
    </div>
    <div class="eventDate">
      {{ eventDate }}
    </div>
    <div class="description">
      {{ data.description }}
    </div>
    <div class="tag">
      <Tag v-for="tag in data.tags" :key="tag" :tag="tag" />
    </div>
  </div>
</template>

<script>
import DateUtil from '../util/dateUtil.js'
import Tag from './Tag.vue'

export default {
  name: 'Card',
  props: {
    data: Object
  },
  components: {
    Tag
  },
  computed: {
    eventDate() {
      let dataList = []
      this.data.eventDate.forEach(d => {
        const eventDate = new Date(d)
        const day = DateUtil.checkDay(eventDate.getDay())
        dataList.push(d + `(${day})`)
      })
      return dataList.join(', ')
    }
  },
  methods: {
    openWebsite(url) {
      window.open(url)
    }
  }
}
</script>

<style scoped>
.card {
  background: #ffffff;
  border: 1px solid #dddddd;
  border-radius: 3px;
  padding: 10px;
  -webkit-column-break-inside: avoid;
  page-break-inside: avoid;
  break-inside: avoid;
  margin-bottom: 10px;
  transition: 0.2s;
  color: #2c3e50;
}

.card:hover {
  background: #ff1493 !important;
  cursor: pointer;
  color: #ffffff !important;
}

.card.now {
  background: #FFF05A;
}

.card > .name {
  font-size: 1.2rem;
  font-weight: bold;
}

.card > .eventDate {
  padding: 3px;
}

.card > .description {
  padding: 3px 3px 10px 3px;
}
</style>
