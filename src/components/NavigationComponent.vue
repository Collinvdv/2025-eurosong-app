<template>
    <nav>
      <ul>
        <li 
            v-for="(item, index) in items" 
            :key="index" 
            class="c-navigation__link"
            @click="setActivePage(item)"
        >
          {{ item }}
        </li>
      </ul>
    </nav>
</template>

<script>
    export default {
        name: "NavigationComponent",
        data() {
            return {
                items: [
                    "home",
                    "artists",
                    "songs",
                    "ranking",
                    "voting"
                ]
            }
        },
        methods: {
            setActivePage(page) {
                this.$emit("setActivePage", page);
            }
        }
    }
</script>