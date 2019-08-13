<template functional>
  <v-card>
    <v-card-title class="headline">
      {{ title }}
    </v-card-title>
    <v-card-actions>
      <v-spacer />
      <v-btn
        color="primary"
        nuxt
        :to="link"
      >
        Read
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "PostCard",
  props: {
    title: {
      type: String,
      default: ""
    },
    link: {
      type: String,
      default: ""
    }
  }
};
</script>
