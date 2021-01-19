<template>
    <div class="container">
        <Navbar />
        <div class="main-content">
            <div class="content-wrapper">
                <Header />
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
                                    <span class="post-author">
                                        par <a href="">{{ article.author.name }}</a>
                                    </span>
                                    <span class="post-date">
                                        le {{ formatDate(article.updatedAt) }}
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
        </div>
        <Footer />
    </div>
</template>

<script lang="js">
export default {
    async asyncData({ $content, params }) {
        const articles = await $content('articles', params.slug)
            .only(['title', 'description', 'img', 'slug', 'author', 'updatedAt'])
            .sortBy('createdAt', 'asc')
            .fetch()

        return {
            articles,
        }
    },
    methods: {
        formatDate(date) {
            const options = { year: 'numeric', month: 'short', day: 'numeric' }
            return new Date(date).toLocaleDateString('fr', options)
        },
    },
}
</script>
