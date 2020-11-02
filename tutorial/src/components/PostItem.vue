<template>
    <div class="post-item" @click="favouritePost(post.id)">
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
    },

    methods: {
        favouritePost(id) {
            this.$emit('favourite', id);
        }
    }
}
</script>

<style lang="scss" scoped>

    .post-item {
        cursor: pointer;

        .user-profile__post {
            background-color: white;
            text-align: left;
            border-radius: 5px;
            margin-bottom: 10px;
            padding: 12px;
            box-sizing: border-box;
            border-bottom: 2px solid #c0c0c0;
            
            &:hover {
                transform: scale(1.01);
                transition: transform .1s;
            }

            .post-item__user {
                font-size: 12px;
                font-weight: bold;
                padding-bottom: 5px;
            }

            .post-item__content {
                h3 {
                    font-weight: normal;
                    font-size: 18px;
                    margin: 0 auto;
                }
                p {
                    color: gray;
                    font-size: 12px;
                    margin: 6px auto;
                }
                span.post-url {
                    a {
                        color: blueviolet;
                        font-size: 12px;
                        text-decoration: none;
                    }
                }
            }
        }
    }
</style>