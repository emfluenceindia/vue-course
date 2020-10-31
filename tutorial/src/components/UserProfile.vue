<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="userprofile__username">@{{user.username}}</h1>
            <div class="user-profile__admin-badge" v-if="user.isAdmin">
                Admin
            </div>
            <div class="user-profile__follower-count">
                {{post_count}} Posts | {{followers}} Followers
           </div>
           <form class="user-profile__create-post" @submit.prevent="createNewPost">
               <h2>New Post</h2>
               <label for="post-title">Post Title</label>
               <input type="text" id="post-title" name="post-title" v-model="postTitle" />
               <label for="post-excerpt">Short Descripton</label>
               <textarea name="post-excerpt" id="post-excerpt" rows="4" v-model="postExcept"></textarea>
               <label for="post-url">Url</label>
               <input type="text" id="post-url" name="post-url" v-model="postUrl" />
               <label for="post-status">Select Status</label>
               <select name="post-status" id="post-status" v-model="selectedStatus">
                   <option v-for="status in postStatuses" :key="status.id" :value="status.value">
                       {{status.display}}
                   </option>
               </select>
               <button>Submit</button>
           </form>
        </div>
        <div class="user-profile__user-posts" v-if="user.posts.length > 0">
            <h1 class="recent-posts">Recent Posts</h1>
            <PostItem 
                v-for="post in user.posts" 
                :key="post.id" 
                :username="user.username" 
                :post="post" 
                @favourite="toggleFavourite" 
            />
        </div>
    </div>
</template>

<script>

import PostItem from "./PostItem";

export default {
    name: 'UserProfile',
    components: {
        PostItem
    },
    data() {
        return {
                selectedStatus: 'publish',
                postTitle: '',
                postExcept: '',
                postUrl: '',

                postStatuses:[
                    {
                        id: 1,
                        value: 'draft',
                        display: 'Save Draft'
                    },
                    {
                        id: 2,
                        value: 'publish',
                        display: 'Publish Immediately'
                    },
                    {
                        id: 3,
                        value: 'schedule',
                        display: 'Schedule Publish'
                    }
                ],

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
        },

        toggleFavourite(id) {
            console.log(id);
        },

        totalPosts() {
            this.post_count = this.user.posts.length;
        },
        
        createNewPost() {
            if( this.postTitle && this.postExcept && this.selectedStatus === 'publish' ) {
                this.user.posts.unshift({
                    id: this.user.posts.length + 1,
                    title: this.postTitle,
                    excerpt: this.postExcept,
                    url: this.postUrl
                });
            }

            this.postTitle = '';
            this.postExcept = '';
            this.postUrl = '';

            this.totalPosts();
        }
    },
    
    mounted() {
        this.followUser();
        this.totalPosts();
        //this.post_count = this.user.posts.length;
    }
}
</script>

<style lang="scss" scoped>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 90%;
    padding:50px 5%;

    .user-profile__user-panel {
        display: flex;
        flex-direction: column;
        margin-right: 50px;
        padding: 20px;
        background-color: white;
        border-radius: 5px;
        text-align: left;

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

        .user-profile__create-post {
            display: flex;
            flex-direction: column;
            padding-top: 20px;

            h2 {
                margin: 0;
                font-weight: normal;
                color: rebeccapurple;
                font-size: 18px;
                padding-bottom: 10px;
            }

            label {
                font-size: 11px;
                padding: 5px 0 2px 0;
                font-weight: bold;
            }

            input[type="text"], textarea {
                padding: 6px;
                border: 1px solid #d3d3d3;
                border-radius: 5px;
                box-sizing: border-box;
                font-family: Avenir, Helvetica, Arial, sans-serif;
            }

            button {
                margin-top: 12px;
                cursor: pointer;
                background-color: rebeccapurple;
                color: white;
                border: 0;
                padding: 10px 0;
                text-transform: uppercase;
                border-radius: 5px;
            }

            select {
                border: 1px solid #d3d3d3;
                font-size: 12px;
                padding: 6px;
                border-radius: 5px;
                box-sizing: border-box;
            }
        }
    }

    .user-profile__user-posts {
        h1.recent-posts {
            font-size: 18px;
            margin-bottom: 8px;
            background-color: rebeccapurple;
            color: white;
            padding: 5px 10px;
            border-radius: 5px;
        }
    }
}











</style>