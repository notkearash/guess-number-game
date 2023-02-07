<template>
    <Container>
        <Game />
    </Container>
</template>

<script>
import Container from "./components/Container.vue";
import Game from "./components/Game.vue";
export default {
    name: "App",
    components: { Container, Game },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto+Mono&display=swap");
#app { font-family: "Roboto Mono", monospace; }
</style>
