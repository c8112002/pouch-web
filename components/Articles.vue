<template>
  <section>
    <div v-for="articles in articlesList" class="tile is-ancestor">
      <div v-for="article in articles" class="tile is-parent is-4">
        <article class="tile is-child box">
          <p class="title">
            <a :href="article.url" target="_blank">
              {{article.title}}
            </a>
          </p>
          <a :href="article.url" target="_blank">
            <figure class="image is-4by3">
              <img :src="imagePath(article)">
            </figure>
          </a>
          <div class="article-menu">
            <edit-button :article_id="article.id" />
            <read-button />
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<script>
import EditButton from '~/components/EditButton.vue'
import ReadButton from '~/components/ReadButton.vue'
import { mapGetters } from 'vuex'
export default {
  components: {
    EditButton,
    ReadButton
  },
  computed: {
    ...mapGetters({
      articlesList: 'articles/articlesList',
      currentLastArticleId: 'articles/currentLastArticleId'
    })
  },
  methods: {
    imagePath(article) {
      return article.imagePath
        ? article.imagePath
        : 'https://bulma.io/images/placeholders/640x480.png'
    }
  }
}
</script>

<style scoped>
/* disable links coloring */
a {
  color: inherit;
  text-decoration: none;
}

.article-menu {
  display: flex;
  justify-content: flex-end;
  margin-top: 10px;
}
</style>
