<template>
  <div>
    <div class="seo-inspect">
      Inspect the HTML source and look at all the juicy SEO meta tags we're
      generating!
    </div>
    <div class="app">
      <div class="app-title">DatoCMS Blog</div>
      <div class="app-subtitle">
        News, tips, highlights, and other updates from the team at DatoCMS.
      </div>
      <article
        v-for="blogPost in result.data.blogPosts"
        :key="blogPost.id"
        class="blogPost"
      >
        <datocms-image
          class="blogPost-image"
          :fade-in-duration="1000"
          :data="blogPost.coverImage.responsiveImage"
        />
        <h6 class="blogPost-title">
          <a
            :href="`https://www.datocms.com/blog/${blogPost.slug}`"
            target="_blank"
            rel="noopener noreferrer"
          >
            {{ blogPost.title }}
          </a>
        </h6>
        <div class="blogPost-excerpt">
          <structured-text :data="blogPost.excerpt" />
        </div>
        <footer class="blogPost-author">
          <datocms-image
            class="blogPost-author-image"
            :data="blogPost.author.avatar.responsiveImage"
          />
          Written by {{ blogPost.author.name }}
        </footer>
      </article>
    </div>
  </div>
</template>

<script setup>
import { useDatoFetch } from "~/lib/datocms";
import { query } from "~/lib/query";

const { data: result } = await useDatoFetch({ query });

// useHead({

// });
</script>

<script>
import { Image, StructuredText, toHead } from "vue-datocms";

export default {
  components: {
    "datocms-image": Image,
    "structured-text": StructuredText,
  }
};
</script>


<style>
* {
  margin: 0;
  padding: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
body {
  font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Helvetica, Arial,
    sans-serif, Apple Color Emoji, Segoe UI Emoji;
  line-height: 1.5;
  color: #333;
}
.app {
  max-width: 750px;
  margin: 0 auto 3em;
}
.app-title {
  font-size: 3em;
  font-weight: bold;
}
.app-subtitle {
  margin-bottom: 4em;
}
.blogPost {
  padding-bottom: 3em;
  border-bottom: 1px solid #eee;
  margin-bottom: 3em;
}
.blogPost-title {
  font-weight: bold;
  font-size: 1.2em;
  margin-bottom: 0.5em;
}
.blogPost-title a {
  color: inherit;
  text-decoration: none;
}
.blogPost-title a:hover {
  text-decoration: underline;
}
.blogPost-excerpt {
  font-size: 0.9em;
  color: #666;
}
.blogPost-image {
  margin-bottom: 2em;
  border-radius: 3px;
}
.blogPost-author {
  display: flex;
  align-items: center;
  font-size: 0.9em;
  margin-top: 1.5em;
  color: #666;
}
.blogPost-author-image {
  border-radius: 50%;
  margin-right: 15px;
  width: 40px;
}
.seo-inspect {
  background: #f5f5f5;
  border-radius: 3px;
  padding: 25px;
  overflow: auto;
  font-size: 11px;
  margin-bottom: 8em;
  text-align: center;
  font-family: "SFMono-Regular", Consolas, "Liberation Mono", Menlo, Courier,
    monospace;
}
</style>