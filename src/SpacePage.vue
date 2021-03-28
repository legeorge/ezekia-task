<template>
  <div class="space-page">
    <h1 class="space-page__title">Space</h1>

    <!-- Add the museum highlight cards based on the data provided below -->

    <div class="space-page__container">
      <museum-highlight
        class="space-page__museum-highlight"
        v-for="(highlight, index) in sortedHighlights"
        :title="highlight.name"
        :image="highlight.image"
        :description="highlight.description"
        :source-type="highlight.sourceType"
        :key="index"
      >
        <template v-slot:badge>
          <div class="space-page__museum-highlight__star" />
        </template>
        <div class="space-page__museum-highlight__quiz" v-if="highlight.quiz">
          <a
            class="space-page__museum-highlight__quiz--decoration"
            :href="highlight.quiz"
          >
            <h2>Take the quiz</h2>
          </a>
        </div>
        <!-- other relevant data can be added -->
      </museum-highlight>
    </div>
  </div>
</template>

<script>
import MuseumHighlight from "./MuseumHighlight";

export default {
  name: "SpacePage",
  components: {
    MuseumHighlight,
  },
  data() {
    return {
      spaceHighlights: [
        {
          date: "2020-04-20 12:20:00",
          description:
            "Asteroids are minor planets, especially of the inner Solar System. Larger asteroids have also been called planetoids.",
          id: 1,
          image: "",
          name: "Asteroids",
        },
        {
          date: "2020-05-20 15:50:00",
          description:
            "A comet is an icy, small Solar System body that, when passing close to the Sun, warms and begins to release gases, a process called outgassing.",
          id: 9,
          image: "",
          name: "Comets",
        },
        {
          date: "2020-05-01 9:22:00",
          description:
            "The term planet is ancient, with ties to history, astrology, science, mythology, and religion.",
          id: 7,
          image: "",
          name: "Planets",
          news: {
            date: "2020-08-18 18:00:00",
            title: "Attend our talk about Jupiter with Dr. Hogarth",
          },
          quiz: "https://planetquiz.space",
        },
        {
          date: "2020-07-05 4:10:00",
          description:
            "A meteor shower is a celestial event in which a number of meteors are observed to radiate, or originate, from one point in the night sky.",
          id: 12,
          image: "",
          name: "Meteor showers",
          news: {
            title: "The Lyrids will peak at on April 21-22 2021, at night",
          },
        },
      ],
      spacePartners: {
        observatory: {
          createdAt: "2020-06-01 11:45:00",
          info:
            "The Mauna Kea Observatories (MKO) are a number of independent astronomical research facilities and large telescope observatories that are located at the summit of Mauna Kea on the Big Island of Hawaiʻi, United States.",
          image: "",
          name: "Mauna Kea Observatories",
        },
      },
    };
  },
  computed: {
    sortedHighlights() {
      return [...this.spaceHighlights].sort((a, b) =>
        a.date > b.date ? -1 : a.date < b.date ? 1 : 0
      );
    },
  },
  beforeMount() {
    for (const {
      createdAt: date,
      info: description,
      image,
      name,
    } of Object.values(this.spacePartners)) {
      const spaceHighlight = {
        date,
        image,
        name,
        description,
        sourceType: "external",
      };
      this.spaceHighlights.push(spaceHighlight);
    }
  },
};
</script>

<style lang="scss" scoped>
// credits for the star icon https://codepen.io/fxm90/pen/yOBWVe

.space-page {
  margin: 0;
  font-family: sans-serif;
  height: 100vh;
  width: auto;
  &__title {
    margin: 0;
    color: #2c3791;
    font-size: 90px;
    text-align: center;
  }
  &__container {
    box-sizing: border-box;
    max-width: 1340px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    padding: 100px;
    grid-gap: 40px;
    @media (max-width: 425px) {
      padding: 124px 30px 190px 30px;
    }
  }
  &__museum-highlight {
    &__quiz {
      margin: auto auto 10px auto;
      &--decoration {
        text-decoration: none;
        color: rgb(64, 88, 116);
      }
    }

    &__star {
      position: relative;

      display: inline-block;
      width: 0;
      height: 0;

      margin-left: 0.9em;
      margin-right: 0.9em;
      margin-bottom: 1.2em;

      border-right: 0.3em solid transparent;
      border-bottom: 0.7em solid #fc0;
      border-left: 0.3em solid transparent;

      /* Controlls the size of the stars. */
      font-size: 24px;

      &:before,
      &:after {
        content: "";

        display: block;
        width: 0;
        height: 0;

        position: absolute;
        top: 0.6em;
        left: -1em;

        border-right: 1em solid transparent;
        border-bottom: 0.7em solid #fc0;
        border-left: 1em solid transparent;

        transform: rotate(-35deg);
      }

      &:after {
        transform: rotate(35deg);
      }
    }
  }
}
</style>
