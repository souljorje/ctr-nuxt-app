<template>
  <div>
    <div class="display-2">
      {{ title }}
    </div>
    <no-ssr>
      <v-img
        :src="imgSrc"
        :lazy-src="imgThumb"
        class="grey lighten-2"
        max-height="400"
      />
    </no-ssr>
    <p class="text-justify">
      {{ body }}
    </p>
  </div>
</template>

<script>
import isNumber from "lodash.isnumber";

export default {
  validate({ params }) {
    return isNumber(Number(params.id));
  },
  data: () => ({
    title: "",
    body: "",
    imgSrc: "",
    imgThumb: ""
  }),
  mounted() {
    this.getImage();
  },
  methods: {
    async getImage() {
      const { id } = this.$route.params;
      try {
        const image = await $axios.$get(`/photos/${id}`);
        this.imgSrc = image.url;
        this.imgThumb = image.thumbnailUrl;
      } catch (err) {
        console.log("error fetching img");
      }
    }
  },
  async asyncData({ app, params, error }) {
    const { id } = params;
    const { $axios } = app;
    try {
      const post = await $axios.$get(`/posts/${id}`);
      const { title, body } = post;
      return {
        title,
        body
      };
    } catch (err) {
      console.log(err);
      const { statusCode } = err.response;
      error({ statusCode });
    }
  }
};
</script>

<style lang="scss">
</style>
