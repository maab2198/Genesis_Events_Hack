<template>
  <div class="events">
    <banner />

    <h2 id="events" class="events__title secondary-title">
      Найбліжчі події
    </h2>
    <div class="events__content">
      <ul class="events__tags">
        <li
          v-for="tag of getTags"
          :key="tag"
          class="events__tag"
          @click="filterTag(tag)"
        >
          tag
        </li>
      </ul>
      <event-list :events="getEventsInitial" />
    </div>
  </div>
</template>

<script>
import { mapGetters, mapMutations } from 'vuex';

export default {
  computed: {
    ...mapGetters([
      'getEvents',
      'getEventsInitial',
      'getTags',
    ]),
  },
  methods: {
    ...mapMutations([
      'setEvents',
      'setEventsInitial',
    ]),
    filterTag(tag) {
      this.setEvents(
        this.getEventsInitial.filter(item => (
          item.tags.includes(tag)
        ))
      );
    }
  },
  // eslint-disable-next-line vue/order-in-components
  async fetch() {
    const data = await fetch(
      'https://kyiv-events-b93ca-default-rtdb.europe-west1.firebasedatabase.app/events.json'
    ).then((res) => res.json())
    const entries = Object.entries(data)


    // this.$store.dispatch('setEvents', Object.values(data))
    // this.$store.dispatch('setEventsInitial', Object.values(data))

    const eventsList = entries.map((obj) => {
      obj[1].id = obj[0]

      return obj[1]
    })
    this.$store.dispatch('setEventsInitial',  eventsList)
    this.$store.dispatch('setEvents', eventsList)
  },
}
</script>

<style lang="scss" scoped>
  @import '@/assets/scss/_vars.scss';

  .events {
    &__content {
      padding-left: $container_padding;
      padding-right: $container_padding;
    }

    &__tags {
      display: flex;
      align-items: center;
      margin-bottom: 32px;
    }

    &__tag {
      background-color: $purple-navy;
      color: $text;
      padding: 4px 8px;
      margin-right: 8px;
      border-radius: 8px;
      text-align: center;
      cursor: pointer;
    }
    
    &__title {
      padding: $container_padding;
      margin-top: 64px;
    }

  }
</style>


