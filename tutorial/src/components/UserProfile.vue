<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="userprofile__username">{{user.username}}</h1>
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
                followers: 0,
                user: {
                    id: 1,
                    username: 'emfl_api',
                    url: 'https://twitter.com/emfl_api',
                    firstName: 'Subrata',
                    lastName: 'Sarkar',
                    email: 'subrata@emfluence.com',
                    isAdmin: false
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
}

h1 {
    margin: 0;
    padding: 0;
    font-size: 160%;
    font-weight: normal;
    text-align: left;
}

.user-profile__follower-count {
    text-align: left;
    font-size: 84%;
}


</style>