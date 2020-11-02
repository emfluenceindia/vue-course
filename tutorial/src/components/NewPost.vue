<template>
    <div>
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
</template>

<script>
export default {
    name: "NewPost",
    props: {
        currentUser: {
            type: Object,
            required: true
        }
    },
    data() {
        return  {
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
        }
    },
    computed: {
    },
    watch: {
    },
    methods: {
        createNewPost() {
            const posts = this.currentUser.posts;
            posts.push({
                id: posts.length + 1,
                title: this.postTitle,
                excerpt: this.postExcept,
                url: this.postUrl

            });

            this.postTitle = '';
            this.postExcept = '';
            this.postUrl = '';

            this.$emit( 'newposts', this.currentUser );
            this.$emit( 'postcount', posts.length );
        }
    }
}
</script>

<style lang="scss" scoped>
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
</style>