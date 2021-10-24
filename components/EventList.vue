<template>
  <div>
    <p v-if="!events.length">No events</p>
    <ul v-else class="events-list">

      <li
        v-for="event of historyList"
        :key="event.id"
        class="events-list__item"
      >
        <div class="events-list__img">
          <img 
            :src="event.img || require('@/assets/img/img-2.png')"
            alt="">
        </div>
        <div class="events-list__description">
          <h3 class="events-list__title">
            {{ event.title }}
          </h3>
          <p class="events-list__text">
            {{ event.description.slice(0, 150) }}...
          </p>
          <div class="events-list__bottom">
            <ul class="events-list__tags">
              <li
                v-for="tag of event.tag"
                :key="tag"
                class="events-list__tag"
              >
                {{ tag }}
              </li>
            </ul>
            <div class="events-list__date">
              {{ $dayjs(event.date).format('DD.MM.YYYY') }}
            </div>
          </div>
        </div>
      </li>
    </ul>
    <div class="pagination">
      <v-pagination
        @input="updatePage"
        v-model="page"
        :length="pagesCount"
        prev-icon="mdi-menu-left"
        next-icon="mdi-menu-right"
      ></v-pagination>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    events: {
      type: Array,
      required: true,
    }
  },
  data: () => ({
    page: 1,
    pageSize: 2,
    historyList: [],
}),
  computed: {
    pagesData() {
      return this.events
    },
    pagesCount() {
      return this.pagesData.length > 2 ? this.pagesData.length / 2 : 1;
    },
    pages() {
			if (this.pageSize == null || this.pagesCount == null) return 0;
			return Math.ceil(this.pagesCount / this.pageSize);
		}
  },
  created() {
		this.initPage();
		this.updatePage(this.page);
	},
  methods: {
    eventClickHandler(eventId) {
      console.log(eventId);
      this.$router.push('event/' + eventId)
    },
    initPage() {
			this.pagesCount = this.pagesData.length;
			if (this.pagesCount < this.pageSize) {
				this.historyList = this.pagesData;
			} else {
				this.historyList = this.pagesData.slice(0, this.pageSize);
			}
		},
		updatePage(pageIndex) {
			const start = (pageIndex - 1) * this.pageSize;
			const end = pageIndex * this.pageSize;
			this.historyList = this.pagesData.slice(start, end);
			this.page = pageIndex;
		}
  },
}
</script>

<style lang="scss">
  @import '@/assets/scss/_vars.scss';

  .events-list {
    &__item {
      display: flex;
      flex-direction: column;
      padding: 24px 0;
      margin-bottom: 32px;
      max-width: 100%;
      cursor: pointer;

      @media (min-width: 769px) {
        flex-direction: row;

        &:nth-child(even) {
          flex-direction: row-reverse;

          .events-list__img {
            margin-right: 16px;
            margin-left: 32px;
          }
        }
      }
    }

    &__img {
      position: relative;
      height: fit-content;
      width: 100%;
      margin-bottom: 32px;
      flex-shrink: 0;

      @media (min-width: 769px) {
        max-width: 25%;
        margin-right: 48px;
        margin-bottom: 0;
      }

      &::before {
        content: '';
        position: absolute;
        width: 100%;
        height: 100%;
        top: -8px;
        right: -16px;
        background-color: $tangerine;
        z-index: 0;
      }

      img {
        position: relative;
        z-index: 1;
        width: 100%;
        background: $text;
      }
    }

    &__description {
      display: flex;
      flex-direction: column;
    }

    &__title {
      margin-bottom: 16px;
      font-size: 32px;
      font-weight: normal;
      line-height: 100%;
      color: $tangerine;

      @media (min-width: 769px) {
        margin-bottom: 32px;
        font-size: 50px;
      }
    }
    
    &__text {
      color: $text;
    }
    &__bottom {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      margin-top: auto;
    }
    &__tags {
      display: flex;
      gap: 8px;
      max-width: 50%;
      margin-right: 16px;
    }
    &__tag {
      background-color: $purple-navy;
      color: $text;
      padding: 4px 8px;
      border-radius: 8px;
      text-align: center;
    }
    &__date {
      color: $tangerine;
    }
  }

</style>
