<script>
import { useStyle } from 'primevue/usestyle';
import { ObjectUtils } from 'primevue/utils';

const styles = `
.p-icon {
    display: inline-block;
}

.p-icon-spin {
    -webkit-animation: p-icon-spin 2s infinite linear;
    animation: p-icon-spin 2s infinite linear;
}

@-webkit-keyframes p-icon-spin {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg);
    }
    100% {
        -webkit-transform: rotate(359deg);
        transform: rotate(359deg);
    }
}

@keyframes p-icon-spin {
    0% {
        -webkit-transform: rotate(0deg);
        transform: rotate(0deg);
    }
    100% {
        -webkit-transform: rotate(359deg);
        transform: rotate(359deg);
    }
}
`;

const { load: loadStyle } = useStyle(styles, { name: 'baseicon', manual: true });

export default {
    name: 'BaseIcon',
    props: {
        label: {
            type: String,
            default: undefined
        },
        spin: {
            type: Boolean,
            default: false
        }
    },
    beforeMount() {
        loadStyle(undefined, { nonce: this.$config?.csp?.nonce });
    },
    methods: {
        pti() {
            const isLabelEmpty = ObjectUtils.isEmpty(this.label);

            return {
                class: [
                    'p-icon',
                    {
                        'p-icon-spin': this.spin
                    }
                ],
                role: !isLabelEmpty ? 'img' : undefined,
                'aria-label': !isLabelEmpty ? this.label : undefined,
                'aria-hidden': isLabelEmpty
            };
        }
    },
    computed: {
        $config() {
            return this.$primevue?.config;
        }
    }
};
</script>
