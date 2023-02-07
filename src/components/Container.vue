<template>
    <div class="body">
        <slot></slot>
    </div>
</template>

<style>
.body {
    display: -webkit-box;
    display: -moz-box;
    display: -ms-flexbox;
    display: -webkit-flex;
    display: flex;
    flex-direction: row;
    background-position: 50%;
    background-size: cover;
    background-repeat: no-repeat;
    position: relative;
    min-height: 100vh;
}

@media screen and (max-width: 520px) {
    .body {
        display: flex;
        flex-wrap: nowrap;
        flex-direction: column;
    }
}
</style>
