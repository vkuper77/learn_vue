<template>
  <div class="container pt-1">
    <div class="card">
      <TheHeader :title="now"/>
      <span>Открыто: <strong>{{ openRate }}</strong> | Прочитано: <strong>{{ readRate }}</strong></span>
    </div>
    <app-news
      v-for="item in news"
      :title="item.title"
      :text="item.text"
      :is-open="item.isOpen"
      :was-read="item.wasRead"
      :key="item.id"
      :id="item.id"
      @open-news="openNews"
      @read-news="readNews"
      @unmark="unreadNews"
    ></app-news>
  </div>
</template>

<script>
import AppNews from '@/components/AppNews'
import TheHeader from '@/components/TheHeader'

export default {
  data () {
    return {
      now: new Date().toLocaleDateString(),
      news: [
        {
          id: 1,
          title: 'Конгрессмены США призвали немедленно ввести санкции против России',
          text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Debitis, libero!',
          isOpen: false,
          wasRead: false
        },
        {
          id: 2,
          title: 'Что показали на Неделе моды классические бренды мужской одежды',
          text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Debitis, libero!',
          isOpen: false,
          wasRead: false
        }
      ],
      openRate: 0,
      readRate: 0
    }
  },
  provide () {
    return {
      title: 'Список всех новостей',
      news: this.news
    }
  },
  methods: {
    openNews () {
      this.openRate++
    },
    readNews (id) {
      const idx = this.news.findIndex(news => news.id === id)
      this.news[idx].wasRead = true
      this.readRate++
    },
    unreadNews (id) {
      const news = this.news.find((news) => news.id === id)
      news.wasRead = false
      this.readRate--
    }
  },
  components: {
    'app-news': AppNews,
    TheHeader
  }
}

</script>
