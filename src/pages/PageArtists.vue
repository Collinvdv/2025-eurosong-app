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
    </div>
</template>

<script>
    export default {
        name: "PageArtists",
        mounted() {
            console.log("get some data from the API");
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
                artists: []
            }
        }
    }
</script>

<style scoped>
    table {
        margin: 0 auto;
    }
</style>