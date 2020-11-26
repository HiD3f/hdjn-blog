<template>
    <div class="headline-post">
        <div>
            <span class="post-title">{{ article.title }}</span>
        </div>
        <div>
            <span class="post-date">{{ article.updatedAt }}</span>
            <span class="post-authot">
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
</template>
