<template>
    <div>
        <h1>
            Artists
        </h1>

        <table border="1">
            <tr>
                <th>
                    Id
                </th>
                <th>
                    Name
                </th>
            </tr>

            <tr v-for="artist in artists" :key="artist.artist_id">
                <td>
                    {{ artist.artist_id }}
                </td>
                <td>
                    {{ artist.name }}
                </td>
            </tr>
        </table>

        <hr>

        <label for="input_new_name">
            New name
        </label>
        <input id="input_new_name" type="text" v-model="newArtist">

        <button @click="addArtists()">
            Add new artists
        </button>
    </div>
</template>

<script>
    export default {
        name: "PageArtists",
        mounted() {
            fetch("http://localhost:3000/artists", {
                method: "GET"
            })
                .then((data) => {
                    return data.json();
                })
                .then((artistsApi) => {
                    this.artists = artistsApi;
                })
        },
        data() {
            return {
                artists: [],
                newArtist: ""
            }
        },
        methods: {
            addArtists() {
                fetch("http://localhost:3000/artists", {
                    method: "POST",
                    headers: {
                        'Accept': 'application/json',
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({
                        name: this.newArtist
                    })
                })
                    .then((data) => {
                        return data.json();
                    })
                    .then((_newArtist) => {
                        console.log(_newArtist);
                    })
            }
        }
    }
</script>

<style scoped>
    table {
        margin: 0 auto;
    }
</style>