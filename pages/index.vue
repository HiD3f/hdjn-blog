<template>
    <div class="container">
        <Header />
        <div class="main-content">
            <div class="headline">
                <div
                    v-for="article of articles"
                    :key="article.slug"
                    class="headline-post"
                >
                    <NuxtLink
                        :to="{
                            name: 'slug',
                            params: { slug: article.slug },
                        }"
                    >
                        <div>
                            <div>
                                <span class="post-title">{{ article.title }}</span>
                            </div>
                            <div>
                                <span class="post-date">{{
                                    article.updatedAt
                                }}</span>
                                <span class="post-author">
                                    by <a href="">{{ article.author.name }}</a>
                                </span>
                            </div>
                            <div>
                                <p class="post-excerpt">
                                    {{ article.description }}
                                </p>
                            </div>
                            <div>
                                <a class="read-post" href="">Read more</a>
                            </div>
                        </div>
                    </NuxtLink>
                </div>
            </div>
        </div>
        <Footer />
    </div>
</template>

<script lang="js">
export default {
    async asyncData({ $content, params }) {
        const articles = await $content('articles', params.slug)
            .only(['title', 'description', 'img', 'slug', 'author'])
            .sortBy('createdAt', 'asc')
            .fetch()

        return {
            articles,
        }
    },
}
</script>
