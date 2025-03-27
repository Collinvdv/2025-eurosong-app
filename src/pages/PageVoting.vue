<template>
    <div>
        {{ songs[activeSongIndex].artists.name }}
        -
       {{ songs[activeSongIndex].name }}

       <button @click="prevSong()">
        prev
       </button>

       <button @click="nextSong()">
        next
       </button>

        <button v-for="(button, btnIndex) in buttons" :key="btnIndex" @click="addVote(btnIndex)" :disabled="button.disabled">
            Add {{ button.amountOfPoints }} points
        </button>
    </div>
</template>

<script>
    export default {
        name: "PageVoting",
        data() {
            return {
                songs: [],
                activeSongIndex: 0,
                buttons: [
                    {
                        amountOfPoints: 2,
                        disabled: false
                    },
                    {
                        amountOfPoints: 4,
                        disabled: false
                    },
                    {
                        amountOfPoints: 8,
                        disabled: false
                    },
                ]
            }
        },
        mounted() {
            this.getSongs();
        },
        methods: {
            addVote(btnIndex) {
                fetch("http://localhost:3000/votes", {
                    method: "POST",
                    headers: {
                        'Accept': 'application/json',
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({
                        voter_id: 1,
                        song_id: this.songs[this.activeSongIndex].song_id,
                        points: this.buttons[btnIndex].amountOfPoints
                    })
                })
                    .then((data) => {
                        return data.json();
                    })
                    .then(() => {
                        this.buttons[btnIndex].disabled = true;

                        let amountOfButtonsEnabled  = this.buttons.filter((button) => button.disabled == false).length;
                         
                        if (amountOfButtonsEnabled == 0) {
                            this.$emit("setActivePage", "ranking");
                        }
                    })
            },
            getSongs() {
                fetch(" http://localhost:3000/songs", {
                    method: "GET"
                })
                    .then((response) => response.json())
                    .then((_songs) => {
                        this.songs = _songs;
                    });
            },
            prevSong() {
                this.activeSongIndex--;
            },
            nextSong() {
                this.activeSongIndex++;
            },
        }
    }
</script>