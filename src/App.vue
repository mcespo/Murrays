<template>
    <main id="app">
        <MurrayContainer />
    </main>
</template>
<script>
import MurrayContainer from "./components/MurrayContainer.vue";

export default {
    name: "app",
    components: {
        MurrayContainer
    }
};
</script>

<style lang="scss">
:root {
    --color-grey20: hsl(0, 0%, 20%);
    --color-grey80: hsl(0, 0%, 88%);
    --color-grey90: hsl(0, 0%, 98%);
    --color-white: hsl(0, 100%, 100%);
    --color-teal40: hsl(171, 94%, 43%);
    --color-teal30: hsl(171, 94%, 35%);
    --color-green50: hsl(139, 68%, 49%);
    --color-green40: hsl(139, 68%, 41%);
    --color-fuchsia50: hsl(348, 99%, 61%);
}

// sitewide styles
html, body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: var(--color-grey20);
    background-color: var(--color-grey90);
}

// buttons
.button {
    cursor: pointer;
    border: 0px;
    border-radius: 3px;
    padding: 12px 14px;
    color: var(--color-white);
    font-size: 13px;
    text-align: center;
    box-shadow: none;
    line-height: normal;
    transition: background-color 200ms;
    &__reset {
        background-color: var(--color-teal40);
        border: 1px solid var(--color-teal30);
        margin-right: 10px;
        &:hover {
            background-color: var(--color-teal30);
        }
    }
    &__save {
        background-color: var(--color-green50);
        border: 1px solid var(--color-green40);
        margin-right: 20px;
        &:hover {
            background-color: var(--color-green40);
        }
    }
}
</style>
