<template>
  <div class="card" @click="openWebsite(data.url)" :class="eventStatus(data.status)">
    <div class="name">
      {{ data.name }}
    </div>
    <div class="eventDate" v-html="eventDate"></div>
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
    /**
     * 開催日付のフォーマット
     */
    eventDate() {
      let dataList = []
      this.data.eventDate.forEach(d => {
        const eventDate = new Date(d)
        const day = DateUtil.checkDay(eventDate.getDay())
        dataList.push(d + `(${day})`)
      })
      return dataList.join(', ')
    },
    
  },
  methods: {
    /**
     * イベントクリック時の処理
     */
    openWebsite(url) {
      window.open(url)
    },

    /**
     * イベントのステータスチェック処理（当日、未来、過去）
     */
    eventStatus(status) {
      switch(status) {
        case 1:
          return 'today'
        case 2:
          return 'future'
        case 3:
          return ''
      }
    }
  }
}
</script>

<style scoped>
.card {
  background: #4ea0ae;
  /* border: 1px solid #dddddd; */
  border-radius: 3px;
  padding: 10px;
  margin-bottom: 10px;
  transition: 0.2s;
  color: #2c3e50;
}

.card:hover {
  background: #fa26a0 !important;
  cursor: pointer;
  color: #ffffff !important;
}

.card.today {
  background: #fa26a0 !important;
  cursor: pointer;
  color: #ffffff !important;
}

.card.future {
  background: #fff48f;
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
