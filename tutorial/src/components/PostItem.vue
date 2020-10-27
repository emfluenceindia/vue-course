<template>
    <div class="post-item">
        <div class="user-profile__post">
            <div class="post-item__user">
                @{{username}}
            </div>
            <div class="post-item__content">
                <h3>{{ post.title }}</h3>
                <p>{{ post.excerpt }}</p>
                <span v-bind:title="post.title" class="post-url">
                    <a target="_blank" v-bind:href="post.url">{{ post.url }}</a>
                </span>
            </div>
        </div>
    </div>    
</template>

<script>
export default {
    name: 'PostItem',
    props: {
        username: {
            type: String,
            required: true
        },
        post: {
            type: Object,
            required: true
        }
    }
}
</script>

<style>
    .user-profile__post {
        border: 1px solid #989898;
        text-align: left;
        border-radius: 5px;
        margin-bottom: 5px;
        padding: 6px;
    }

    .user-profile__post h3 {
        font-weight: normal;
        font-size: 14px;
        margin: 0 auto;
    }

    .user-profile__post p {
        color: gray;
        font-size: 12px;
        margin: 6px auto;
    }

    h1.recent-posts {
        font-size: 18px;
        margin-bottom: 8px;
        background-color: rebeccapurple;
        color: white;
        padding: 5px 10px;
        border-radius: 5px;
    }

    .post-url a {
        color: blueviolet;
        font-size: 12px;
        text-decoration: none;
    }
</style>