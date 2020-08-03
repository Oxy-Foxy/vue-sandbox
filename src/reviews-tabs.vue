<template>
  <div>
    <span
      class="tab"
      v-for="(tab, i) in tabs"
      :key="i"
      @click="activeTab = tab"
      :class="{ activeTab: activeTab === tab }"
      >{{ tab }}</span
    >
    <div v-show="activeTab === 'Reviews'">
      <h2>Reviews</h2>
      <p v-if="!reviews.length">No reviews yet</p>
      <ul>
        <li v-for="(item, i) in reviews" :key="i">
          <div>{{ item.name }}</div>
          <div>{{ item.rating }}</div>
          <div>{{ item.review }}</div>
          <div>{{ item.recomend }}</div>
        </li>
      </ul>
    </div>
    <product-review
      @review-submitted="emitSubmitEvent"
      v-show="activeTab === 'Make a review'"
    ></product-review>
  </div>
</template>
<script>
  import productReview from './product-review';

  export default {
    name: 'reviews-tabs',
    components: { productReview },
    props: {
      reviews: {
        type: Array,
      },
    },
    data() {
      return {
        tabs: ['Reviews', 'Make a review'],
        activeTab: 'Reviews',
      };
    },
    methods: {
      emitSubmitEvent(review) {
        this.$emit('review-submitted', review);
      },
    },
  };
</script>
