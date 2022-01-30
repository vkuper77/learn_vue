<template>
  <div class="card">
    <h3>{{ title }}</h3>
    <app-button
      @action="open"
    >{{ isNewOpen ? 'Закрыть' : 'Открыть' }}
    </app-button>
    <app-button
      color="danger"
      v-if="wasRead"
      @action="$emit('unmark', id)">
      Отметить непрочитанной
    </app-button>
    <div v-if="isNewOpen">
      <hr/>
      <p v-if="isNewOpen">{{ text }}</p>
      <app-button
        v-if="!wasRead"
        @action="mark"
        color="primary">
        Прочесть новость
      </app-button>
      <app-news-list></app-news-list>
    </div>
  </div>
</template>

<script>
import AppButton from '@/components/AppButton'
import AppNewsList from '@/components/AppNewsList'
export default {
  // props:['title'],
  emits: {
    'open-news': null,
    'read-news' (id) {
      if (id) {
        return true
      }
      console.warn('Нет параметра id для emit read-news')
      return false
    },
    unmark: null
  },
  props: {
    wasRead: Boolean,
    title: { type: String, required: true },
    text: String,
    id: Number,
    isOpen: {
      type: Boolean,
      required: false,
      default: false,
      validator (value) {
        return value === true || value === false
      }
    }
  },
  data () {
    return {
      isNewOpen: this.isOpen
    }
  },
  methods: {
    open () {
      this.isNewOpen = !this.isNewOpen
      if (this.isNewOpen) {
        this.$emit('open-news')
      }
    },
    mark () {
      this.isNewOpen = false
      this.$emit('read-news', this.id)
    }
  },
  components: { AppButton, AppNewsList }
}
</script>
