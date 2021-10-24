<template>
  <div>
    <h1>{{ document.title }}</h1>
    <p>{{ document.description }}</p>
    <nuxt-content :document="document" />
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    const slug = params.slug;
    const [document] = await $content(slug)
      .fetch()
      .catch((err) => {
        error({ statusCode: 404, message: "Page not found" });
      });

    return {
      document,
    };
  },
};
</script>
