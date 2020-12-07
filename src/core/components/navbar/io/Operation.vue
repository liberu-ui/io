<script>
import { mapState } from 'vuex';
import formatDistance from '@enso-ui/ui/src/modules/plugins/date-fns/formatDistance';

export default {
    name: 'Operation',

    props: {
        operation: {
            type: Object,
            required: true,
        },
    },

    data: () => ({
        end: true,
    }),

    computed: {
        ...mapState(['enums']),
        elapsed() {
            return formatDistance(this.operation.createdAt);
        },
        remaining() {
            return this.operation.estimatedEnd
                ? formatDistance(this.operation.estimatedEnd)
                : null;
        },
    },

    methods: {
        toggle() {
            this.end = !this.end;
        },
    },

    render() {
        return this.$scopedSlots.default({
            elapsed: this.elapsed,
            end: this.end,
            events: {
                click: () => this.$emit('cancel', this.operation),
            },
            ioTypes: this.enums.ioTypes,
            operation: this.operation,
            remaining: this.remaining,
            toggle: this.toggle,
        });
    },
};
</script>
