<template>
    <div>
        <h1>{{ article.title }}</h1>
        <p>publié le {{ formatDate(article.updatedAt) }}</p>

        <article>
            <nuxt-content :document="article" />
        </article>
    </div>
</template>

<script>
export default {
    async asyncData({ $content, params }) {
        const article = await $content('articles', params.slug).fetch()

        return { article }
    },
    methods: {
        formatDate(date) {
            const options = { year: 'numeric', month: 'long', day: 'numeric' }
            return new Date(date).toLocaleDateString('fr', options)
        },
    },
}
</script>
