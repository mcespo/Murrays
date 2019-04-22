<template>
<div>
    <section class="action-bar">
        <button class="button button__reset" @click="resetList">Reset</button>
        <button class="button button__save">Save changes</button>
    </section>
    <div class="container">
        <!-- if you have the time, consider building the display modal -->
        <aside class="undo-save">New live on the page order is saved. <a href="#">Undo Save</a></aside>
        <section class="section section__queue" ref="queue">
            <h1 class="section-title">Queue</h1>
            <draggable group="posts" class="section-card-container" tag="div" v-model="murrays">
                    <div v-for="murray in murrays" :key="murray.id" class="card">
                        <figure class="card-media">
                            <img :src="murray.media" alt="image of Bill Murry giving an arresting smile">
                        </figure>
                        <article class="card-info">
                            <h2 class="card-info_title">{{murray.title}}</h2>
                            <p class="card-info_author">{{murray.author}}</p>
                            <p class="card-info_date">Published {{murray.date}}</p>
                            <span class="card-info_placement">Not placed</span>
                        </article>
                    </div>
            </draggable>
        </section>
        <section class="section section__live" ref="live">
            <h1 class="section-title">Live on the page</h1>
            <draggable group="posts" class="section-card-container" tag="div" v-model="orderedMurrays">
                    <div v-for="(murray, index) in orderedMurrays" :key="murray.id" class="card">
                        <figure class="card-media">
                            <img :src="murray.media" alt="image of Bill Murry giving an arresting smile">
                        </figure>
                        <article class="card-info">
                            <h2 class="card-info_title">{{murray.title}}</h2>
                            <p class="card-info_author">{{murray.author}}</p>
                            <p class="card-info_date">Published {{murray.date}}</p>
                            <span class="card-info_placement" v-if="index === 0">Hero story</span>
                            <span class="card-info_placement" v-else>Slot {{index}}</span>
                        </article>
                    </div>
            </draggable>
        </section>
    </div>
</div>
</template>

<script>
import draggable from "vuedraggable";

export default {
    name: "MurrayContainer",
    components: {
        draggable
    },
    data() {
        return {
            murrays: [
                {
                    id: 1,
                    media: "http://www.fillmurray.com/200/300",
                    title: "Must go faster... go, go, go, go, go!",
                    author: "David Levinson",
                    date: "Mar 12, 2019 at 8:55 am"
                },{
                    id: 2,
                    media: "http://www.fillmurray.com/g/300/300",
                    title: "Is this my espresso machine?",
                    author: "Alistair Hennessey",
                    date: "Feb 23, 2019 at 1:05 pm"
                },{
                    id: 3,
                    media: "http://www.fillmurray.com/g/300/400",
                    title: "What do they got in there? King Kong?",
                    author: "Dr. Ian Malcolm",
                    date: "Feb 12, 2019 at 11:35 am"
                },{
                    id: 4,
                    media: "http://www.fillmurray.com/300/300",
                    title: "So you two dig up, dig up dinosaurs?",
                    author: "Dr. Ian Malcolm",
                    date: "Feb 2, 2019 at 12:05 pm"
                },{
                    id: 5,
                    media: "http://www.fillmurray.com/g/200/300",
                    title: "You really think you can fly that thing?",
                    author: "David Levinson",
                    date: "Jan 2, 2019 at 10:05 am"
                }
            ],
            orderedMurrays: []
        }
    },
    methods: {
        resetList() {
            Object.assign(this.$data, this.$options.data());
        }
        // resetSave() {
        //     console.log(this.$refs.undo)
        // }
    }
};
</script>

<style scoped lang="scss">

// area action bar
.action-bar {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    width: 100%;
    height: 80px;
    border-bottom: 1px solid var(--color-grey80);
}

// container section
.container {
    position: relative;
    background-color: var(--color-grey90);
    display: grid;
    grid-gap: 2em 1em;
    justify-content: center;
    padding: 1em 2em;
    grid-template-columns: repeat(2, 1fr);
    @include breakpoint(fromLarger) {
        grid-template-columns: repeat(2, minmax(500px, 550px));
    }
    .undo-save {
        color: var(--color-white);
        background-color: var(--color-fuchsia50);
        border-radius: 4px;
        padding: 1em 2em;
        z-index: 10;
        width: 400px;
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
        margin-left: auto;
        margin-right: auto;
        opacity: 0;
        transform: translateY(0);
        transition: all 1500ms ease-in-out;
        &.visible {
            opacity: 0.8;
            transform: translateY(-10em);
        }
        a {
            font-weight: bold;
            color: inherit;
        }
    }
    .section {
        display: flex;
        flex-direction: column;
        border: 1px solid var(--color-grey80);
        background-color: var(--color-white);
        padding: 1em 2em;

        // color changes for placement badge
        &__queue {
            .card-info_placement {
                background-color: var(--color-fuchsia50);
            }
        }
        &__live {
            .card-info_placement {
                background-color: var(--color-green50);
            }
        }
        .section-title {
            font-size: 20px;
            @include breakpoint(fromMedium) {
                font-size: 24px;
            }
            margin: 0 0 1em 0;
        }
        .section-card-container {
            height: 100%;
        }

        // card section
        .card {
            align-self: center;
            width: 100%;
            cursor: grab;
            border: 1px solid var(--color-grey80);
            display: flex;
            height: 150px;
            @include breakpoint(fromLarge) {
                max-width: 550px;
            }

            &:active {
                cursor: grabbing;
            }
            &:not(:last-child) {
                margin-bottom: 1em;
            }
            .card-media {
                margin: 0;
                display: none;
                width: 150px;
                height: 100%;
                overflow-y: hidden;
                @include breakpoint(fromLarge) {
                    display: block;
                }
                img {
                    width: 100%;
                }
            }
            .card-info {
                background-color: var(--color-white);
                padding: 1em;
                position: relative;
                flex: 1;
                display: flex;
                flex-direction: column;
                justify-content: flex-end;
                .card-info_title {
                    margin: 0 0 0.5em 0;
                    font-size: 16px;
                    @include breakpoint(fromMedium) {
                        font-size: 18px;
                    }
                }
                .card-info_author {
                    margin: 0 0 0.5em 0;
                }
                .card-info_date {
                    font-size: 12px;
                    display: none;
                    margin: 0;
                    @include breakpoint(fromMedium) {
                        display: block;
                    }
                }
                .card-info_placement {
                    font-size: 0.75em;
                    border-radius: 4px;
                    padding: 4px;
                    color: var(--color-white);
                    position: absolute;
                    right: 3%;
                    top: 3%;
                    // background-color is nested under '.section'
                }
            }
        }
    }
}

</style>
