<template>
    <div class="thumbnail-list">
        <ol :class="classes" :style="styles">
            <thumbnail-list-items
                :cover="cover"
                :contain="contain"
                :fill="fill"
                :min-height="minHeight"
                :height="height"
                :max-height="maxHeight"
                :min-width="minWidth"
                :width="width"
                :max-width="maxWidth">
                <slot />
            </thumbnail-list-items>
        </ol>
    </div>
</template>

<script>
import ThumbnailListItems from './ThumbnailListItems';

export default {

    components: {
        ThumbnailListItems,
    },

    props: {

        cols: [String, Number],

        contain: Boolean,

        cover: Boolean,

        fill: Boolean,

        height: [String, Number],

        minHeight: [String, Number],

        minWidth: [String, Number],

        maxHeight: [String, Number],

        maxWidth: [String, Number],

        rows: [String, Number],

        width: [String, Number],
        

        /*
        fill: Boolean,

        flex: Boolean,

        noFlex: Boolean,

        grid: Boolean,

        wrap: Boolean,

        width: {
            type: [String, Number],
            default: 75
        }
        */

    },

    computed: {

        classes() {
            return {
                'auto-flow-columns': this.rows || !this.cols,
                'auto-flow-rows': this.cols,
            };
        },

        styles() {
            return {
                'grid-template-columns': this.cols ? `repeat(${this.cols}, 1fr)` : undefined,
                'grid-template-rows': this.rows ? `repeat(${this.rows}, 1fr)` : undefined
            };
        }

    }

};
</script>

<style>
.thumbnail-list > ol {
    margin: 0;
    padding: 0;
    display: grid;
    grid-gap: .5rem;
    width: 100%;
}

.thumbnail-list > ol > li {
    display: flex;
    align-content: center;
    justify-content: center;
}

.thumbnail-list .auto-flow-columns {
    grid-auto-flow: column;
}

.thumbnail-list .auto-flow-rows {
    grid-auto-flow: row;
}

.thumbnail-list-contain img {
    width: 100%;
    object-fit: contain;
}

.thumbnail-list-cover img {
    width: 100%;
    object-fit: cover;
}

.thumbnail-list-fill img {
    width: 100%;
    object-fit: fill;
}

.thumbnail-list-item img {
    max-width: 100%;
    max-height: 100%;
}

/*

.thumbnail-list:not(.thumbnail-list-grid) > *:not {
    padding-right: 10px;
    padding-bottom: 10px;
}

.thumbnail-list:not(.thumbnail-list-grid) > *:first-child:last-child {
    padding: 0;
}

.thumbnail-list.thumbnail-list-fill,
.thumbnail-list.thumbnail-list-wrap {
    flex-flow: row wrap;
}

.thumbnail-list.thumbnail-list-noflex > * {
    flex: 0;
}

.thumbnail-list.thumbnail-list-fill > * {
    flex: 1 0 auto;
}

.thumbnail-list.thumbnail-list-wrap > * {
    flex: 0 0 auto;
}

.thumbnail-list.thumbnail-list-flex > * {
    flex: 1;
}

*/
</style>
