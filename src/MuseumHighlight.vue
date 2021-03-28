<template>
  <div class="museum-highlight">
    <!-- Display the available information for the highlight -->
    <template>
      <div
        class="museum-highlight__card"
        :class="`museum-highlight--${sourceType}`"
      >
        <h1 class="museum-highlight__card__title" v-text="title" />
        <img
          v-if="image"
          class="museum-highlight__card__image"
          :src="image"
          :alt="title"
        />
        <p class="museum-highlight__card__description" v-text="description" />
        <div class="museum-highlight__card__badge">
          <slot name="badge" />
        </div>
        <slot />
      </div>
    </template>
  </div>
</template>

<script>
export default {
  name: "MuseumHighlight",
  components: {},
  mixins: [],
  props: {
    title: String,
    description: String,
    image: String,
    sourceType: {
      default: "internal",
      type: String,
    },
  },
  data() {
    return {
      showMore: false,
    };
  },
  // computed: {
  //   newsDate() {
  //     // Highlight's news item date
  //   },
  // },
  methods: {},
  created() {},
};
</script>

<style lang="scss" scoped>
.museum-highlight {
  &__card {
    align-content: center;
    display: flex;
    flex-direction: column;
    width: auto;
    height: 300px;
    border-radius: 4px;
    box-shadow: 3px 3px 3px rgb(0 0 0 / 5%), 3px 3px 3px rgb(0 0 0 / 8%);
    // box-shadow: 3px 3px 6px rgb(0 0 0 / 5%), 1px 1px 20px rgb(0 0 0 / 16%);
    // box-shadow: 3px 3px 6px rgb(0 0 0 / 5%), 1px 1px 20px rgb(0 0 0 / 16%);
    position: relative;
    &__badge {
      position: absolute;
      top: 0;
      right: 0;
      transform: translate(50%, -50%);
    }
    &__title {
      padding: 10px 10px;
    }
    &__image {
      //styling for image
    }
    &__description {
      margin: 10px 10px;
      // in case we have a long description/mobile view and assuming the text could be read in full if you click on the card
      display: -webkit-box;
      -webkit-line-clamp: 4;
      -webkit-box-orient: vertical;
      overflow: hidden;
    }
  }
  &--internal {
    background-color: #f2f2f2;
  }
  &--external {
    background-color: #ceddf9;
  }
}
</style>
