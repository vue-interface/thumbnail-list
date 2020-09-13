<script>
import { unit } from '@vue-interface/utils';

export default {
    
    functional: true,

    props: {
        // contain: Boolean,
        // cover: Boolean,
        // fill: Boolean,
        height: [String, Number],
        maxHeight: [String, Number],
        maxWidth: [String, Number],
        minHeight: [String, Number],
        minWidth: [String, Number],
        width: [String, Number],
    },

    render(h, context) {
        return context.children.map(child => {
            if(child.text) {
                return child;
            }
            
            if(!child.data) {
                child.data = {};
            }

            /*
            ['height', 'minHeight', 'maxHeight', 'width', 'maxWidth', 'maxHeight']
                .forEach(style => {
                    child.data.style = Object.assign({
                        [style]: context.props[style] ? unit(context.props[style]) : undefined
                    }, child.data.style);
                });
            */

            return h('li', {
                style: {
                    /*
                    height: context.props.height ? unit(context.props.height) : undefined,
                    minHeight: context.props.minHeight ? unit(context.props.minHeight) : undefined,
                    maxHeight: context.props.maxHeight ? unit(context.props.maxHeight) : undefined,
                    width: context.props.width ? unit(context.props.width) : undefined,
                    minWidth: context.props.minWidth ? unit(context.props.minWidth) : undefined,
                    maxWidth: context.props.maxWidth ? unit(context.props.maxWidth) : undefined,
                    */
                },
                class: {
                    'thumbnail-list-item': true,
                    /*
                    'thumbnail-list-contain': !!context.props.contain,
                    'thumbnail-list-cover': !!context.props.cover,
                    'thumbnail-list-fill': !!context.props.fill,
                    */
                }
            }, [child]);
        });
    }
};
</script>