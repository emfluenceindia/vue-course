<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="userprofile__username">@{{user.username}}</h1>
            <div class="user-profile__admin-badge" v-if="user.isAdmin">
                Admin
            </div>
            <div class="user-profile__follower-count">
                Followers: {{followers}}
           </div>
        </div>
        <div class="user-profile__user-posts" v-if="user.posts.length > 0">
            <h1 class="recent-posts">Recent Posts</h1>
            <div class="user-profile__post" v-for="post in user.posts" :key="post.id">
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
    name: 'UserProfile',
    data() {
        return {
                followers: 105,
                post_count: 0,
                user: {
                    id: 1,
                    username: 'emfl_api',
                    url: 'https://twitter.com/emfl_api',
                    firstName: 'Subrata',
                    lastName: 'Sarkar',
                    email: 'subrata@emfluence.com',
                    isAdmin: true,
                    posts: [
                    {
                        id: 1,
                        title: 'Traditional Cultural Expression: Durga Puja as an Intangible Cultural Heritage',
                        excerpt: "The definition of tangible cultural heritage is of physical artefacts produced, maintained and transmitted intergenerationally in society, while intangible...",
                        url: 'https://ipgyan.com/traditional-cultural-expression-durga-puja-as-an-intangible-cultural-heritage/'
                    },
                    {
                        id: 2,
                        title: 'Business Requirements in the Modern Digital Age',
                        excerpt: "India is the land of festivals, and if you are Bengali, then the first thing that comes...",
                        url: 'https://ipgyan.com/business-requirements-in-the-modern-digital-age/'
                    },
                    {
                        id: 3,
                        title: 'Intellectual Property Law Considerations of Protecting Laal Paar Shada Shadi',
                        excerpt: "Pop culture has revived the Bengali way of life back to its screen and made it relevant again...",
                        url: 'https://ipgyan.com/intellectual-property-law-considerations-of-protecting-laal-paar-shada-shadi/'
                    },
                ],
                },
            }
    },
    computed: {
        fullName(){
        return `${this.user.firstName} ${this.user.lastName}`;
        },
        fullNameUS(){
        return `${this.user.lastName} ${this.user.firstName}`;
        }
    },

    watch: {
        followers(newFollowerCount, oldFollowerCount) {
        if( newFollowerCount > oldFollowerCount ) {
            //console.log('New follower added');
            //Do something real here...
        }
        }
    },

    methods: {
        followUser() {
            this.followers++;
        }
    },
    
    mounted() {
        this.followUser();
        //this.post_count = this.user.posts.length;
    }
}
</script>

<style>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 90%;
    padding:50px 5%;
}

.user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #666666;
    text-align: left;
}

h1 {
    margin: 0;
    padding: 0;
    font-size: 150%;
    font-weight: normal;
    text-align: left;
}

.user-profile__follower-count {
    margin: 5px 0;
    text-align: left;
    font-size: 84%;
}

.user-profile__admin-badge {
    background-color: rebeccapurple;
    color: white;
    font-size: 80%;
    margin-top: 5px;
    margin-right: auto;
    padding: 4px 10px;
    border-radius: 3px;

}

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