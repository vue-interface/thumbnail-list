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
import { unit } from '@vue-interface/utils';
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

        grid: Boolean,

        height: [String, Number],

        minHeight: [String, Number],

        minWidth: [String, Number],

        maxHeight: [String, Number],

        maxWidth: [String, Number],

        rows: [String, Number],

        width: [String, Number],
        
        wrap: Boolean

    },

    computed: {

        classes() {
            return {
                'thumbnail-list-contain': this.contain,
                'thumbnail-list-cover': this.cover,
                'thumbnail-list-fill': this.fill,
                'thumbnail-list-grid': this.grid,
                'thumbnail-list-wrap': this.wrap,
                'thumbnail-list-auto-flow-columns': !!this.rows
            };
        },

        hasHeight() {
            return !this.minHeight && !this.maxHeight && !this.height;
        },

        hasWidth() {
            return !this.minWidth && !this.maxWidth && !this.width;
        },

        minmax() {
            return unit(this.width) || `minmax(${unit(this.minWidth)}, ${this.maxWidth ? unit(this.maxWidth) : '1fr'})`;
        },

        styles() {
            const wrap = this.grid && this.minmax ? `repeat(${this.cols ? this.cols  : 'auto-fit'}, ${this.minmax})` : undefined;

            return {
                'grid-template-columns': this.grid && this.cols ? `repeat(${this.cols}, 1fr)` : wrap,
                'grid-template-rows': this.grid && this.rows ? `repeat(${this.rows}, 1fr)` : undefined
            };
        }

    }

};
</script>

<style>
.thumbnail-list > ol {
    margin: 0;
    padding: 0;
    width: 100%;
    grid-gap: .5rem;
}

.thumbnail-list > ol:not(.thumbnail-list-grid) {
    display: flex;
}

.thumbnail-list > ol.thumbnail-list-wrap:not(.thumbnail-list-grid) {
    flex-wrap: wrap;
}

.thumbnail-list-grid {
    display: grid;
}

.thumbnail-list > ol > li {
    display: flex;
    align-content: center;
    justify-content: center;
}

.thumbnail-list-auto-flow-columns {
    grid-auto-flow: column;
}

.thumbnail-list-auto-flow-rows {
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
</style>
