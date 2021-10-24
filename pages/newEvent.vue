<template>
  <div class="addEvent">
    <form
      autocomplete="off"
      class="addEvent__form form"
      @submit.prevent="addEvent"
    >
      <div class="form__field">
        <label class="form__label">City</label>
        <input class="form__input" type="text" v-model="data.city" />
      </div>
      <div class="form__field">
        <label class="form__label">Date</label>
        <input class="form__input" type="date" v-model="data.date" />
      </div>
      <div class="form__field">
        <label class="form__label">Description</label>
        <textarea class="form__input" v-model="data.description" />
      </div>
      <div class="form__field">
        <label class="form__label">Image</label>
        <input class="form__input" type="url" v-model="data.img" />
      </div>
      <div class="form__field">
        <label class="form__label">Owner</label>
        <input class="form__input" type="text" v-model="data.owner" />
      </div>
      <div class="form__field">
        <label class="form__label">Payment</label>
        <input class="form__input" type="text" v-model="data.payment" />
      </div>
      <div class="form__field form__field--checkbox">
        <h3 class="form__label">Tags:</h3>
        <label class="form__label form__label--tag" for="movie"
          >#movie
          <input
            class="form__input"
            type="checkbox"
            id="movie"
            value="Movie"
            v-model="data.tag"
          />
        </label>
        <label class="form__label form__label--tag" for="free"
          >#free
          <input
            class="form__input"
            type="checkbox"
            id="free"
            value="Free"
            v-model="data.tag"
          />
        </label>

        <label class="form__label form__label--tag" for="kyiv"
          >#kyiv
          <input
            class="form__input"
            type="checkbox"
            id="kyiv"
            value="Kyiv"
            v-model="data.tag"
          />
        </label>
      </div>
      <div class="form__field">
        <label class="form__label">Title</label>
        <input class="form__input" type="text" v-model="data.title" />
      </div>
      <div class="form__field">
        <label class="form__label">Type</label>
        <input class="form__input" type="text" v-model="data.type" />
      </div>
      <div>
        <button class="form__button" type="submit">Submit</button>
      </div>
    </form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      data: {
        city: '',
        date: '',
        description: '',
        img: '',
        owner: '',
        payment: '',
        tag: [],
        title: '',
        type: '',
      },
    }
  },
  methods: {
    async addEvent() {
      try {
        const response = await fetch(
          'https://kyiv-events-b93ca-default-rtdb.europe-west1.firebasedatabase.app/events.json',
          {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
            },
            body: JSON.stringify(this.data), // body data type must match "Content-Type" header
          }
        )
        console.log(response)
      } catch (err) {
        console.log(err)
      }
    },
  },
}
</script>
<style lang="scss" scoped>
@import '@/assets/scss/_vars.scss';

.addEvent {
  min-height: calc(100vh - 112px);
  display: flex;
  flex-direction: column;
}
</style>