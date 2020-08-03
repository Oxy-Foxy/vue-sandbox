<template>
  <form @submit.prevent="onSubmit">
    <div>
      Please correct this error(s):
      <ul>
        <li v-for="(error, i) in errors" :key="i">
          {{ error }}
        </li>
      </ul>
    </div>
    <p>
      <label>
        <span>Name:</span>
        <input type="text" v-model="name" />
      </label>
    </p>
    <p>
      <label>
        <span>Review:</span>
        <textarea
          name="review"
          id=""
          cols="30"
          rows="10"
          v-model="review"
        ></textarea>
      </label>
    </p>

    <p>
      <label>
        <span>Rating:</span>
        <select v-model.number="rating">
          <option value="1">1</option>
          <option value="2">2</option>
          <option value="3">3</option>
          <option value="4">4</option>
          <option value="5">5</option>
        </select>
      </label>
    </p>
    <h3>
      Would u reccomend this product
    </h3>
    <p>
      <label>
        <input
          name="recomend"
          type="radio"
          value="Recomend"
          v-model="recomend"
        />
        <span>Y</span>
      </label>
      <label>
        <input
          name="recomend"
          type="radio"
          value="Not recomend"
          v-model="recomend"
        />
        <span>N</span>
      </label>
    </p>
    <input type="submit" value="Submit" />
  </form>
</template>

<script>
// import { eventBus } from '@/main.js';
// console.log('bus', eventBus);
let def = {
  rating: 5,
  recomend: 'Recomend',
};
export default {
  name: 'product-review',
  data() {
    return {
      name: null,
      review: null,
      rating: def.rating,
      recomend: def.recomend,
      errors: [],
    };
  },
  methods: {
    onSubmit() {
      this.errors = [];
      // TODO: rewrite validation - make data object with fields, and write loop
      if (this.name && this.review) {
        let productReview = {
          name: this.name,
          review: this.review,
          rating: this.rating,
          recomend: this.recomend,
        };

        this.$emit('review-submitted', productReview);

        this.name = null;
        this.review = null;
        this.rating = def.rating;
        this.recomend = def.recomend;
      } else {
        if (!this.name) this.errors.push('Name required');
        if (!this.review) this.errors.push('Review required');
      }
    },
  },
};
</script>
