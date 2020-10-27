<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="userprofile__username">@{{user.username}}</h1>
            <div class="user-profile__admin-badge" v-if="user.isAdmin">
                Admin
            </div>
            <div class="user-profile__admin-badge" v-if="followers > 100">
                100+ Followers
            </div>
            <div class="user-profile__follower-count">
                Followers: {{followers}}
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
                user: {
                    id: 1,
                    username: 'emfl_api',
                    url: 'https://twitter.com/emfl_api',
                    firstName: 'Subrata',
                    lastName: 'Sarkar',
                    email: 'subrata@emfluence.com',
                    isAdmin: true
                }
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
    }
}
</script>

<style>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
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


</style>