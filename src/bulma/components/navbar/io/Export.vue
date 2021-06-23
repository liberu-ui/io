<template>
    <operation v-bind="$attrs"
        v-on="$listeners">
        <template v-slot:status="{ operation }">
            {{ enums.exportStatuses._get(operation.status) }}
        </template>
        <template v-slot:body="{ operation }">
            <p class="one-line">
                <span class="has-text-weight-bold">
                    {{ i18n('type') }}
                </span> {{ operation.payload.name }}
            </p>
        </template>
        <template v-slot:info="{ operation }">
            <p class="is-flex is-align-items-center">
                <span class="icon has-text-success">
                    <fa icon="check"/>
                </span>
                <span class="has-text-weight-bold has-text-success">
                    {{ operation.payload.entries | shortNumber }}
                </span>
                <span class="icon">
                    /
                </span>
                <span class="has-text-weight-bold has-text-info">
                    {{ operation.payload.total | shortNumber }}
                </span>
            </p>
        </template>
    </operation>
</template>

<script>
import { mapState } from 'vuex';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faCheck } from '@fortawesome/free-solid-svg-icons';
import { shortNumber } from '@enso-ui/mixins';
import Operation from './Operation.vue';

library.add(faCheck);

export default {
    name: 'Export',

    components: { Operation },

    inject: ['i18n'],

    filters: { shortNumber },

    computed: mapState(['enums']),
};
</script>
