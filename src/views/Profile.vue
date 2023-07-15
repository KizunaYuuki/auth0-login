<template>
    <div class="container">
        <div class="row align-items-center profile-header">
            <div class="col-md-2 mb-3">
                <img :src="user?.picture" alt="User's profile picture" class="rounded-circle img-fluid profile-picture" />
            </div>
            <div class="col-md text-center text-md-left">
                <h2>{{ user?.name }}</h2>
                <p class="lead text-muted">{{ user?.email }}</p>
            </div>
        </div>

        <div class="row">
            <highlightjs language="json" :code="JSON.stringify(user, null, 2)" />
        </div>

        <button @click="doSomethingWithToken()">Click</button>
    </div>
</template>

<script lang="ts">
import { useAuth0 } from '@auth0/auth0-vue';
import { onMounted } from 'vue';

export default {
    name: "profile-view",
    setup() {
        const auth0 = useAuth0();

        // Retrieving an Access Token
        const { getAccessTokenSilently } = useAuth0();

        return {
            user: auth0.user,

            doSomethingWithToken: async () => {
                const token = await getAccessTokenSilently();
                // const response = await fetch('https://api.example.com/posts', {
                //     headers: {
                //         Authorization: 'Bearer ' + token
                //     }
                // });
                // const data = await response.json();
                console.log('Retrieving an Access Token\n');
                console.log(token);
            }
        };
    }
};
</script>

