<template>
    <core-i-o>
        <template v-slot:default="{
                isTouch, count, imports, exports
            }">
            <navbar-item icon="sync-alt"
                @click="!isTouch && $refs.navbarItem.toggle();"
                ref="navbarItem"
                v-if="count">
                <template v-slot:desktop-icon="{ icon }">
                    <span class="icon">
                        <fa :icon="icon" spin/>
                    </span>
                </template>
                <template v-slot:sup
                    v-if="count > 0">
                    <span class="has-text-danger">
                        {{ count }}
                    </span>
                </template>
                <template v-slot:default>
                    <div class="operation-list">
                        <a v-for="operation in imports"
                            :key="operation.id"
                            class="navbar-item">
                            <operation :operation="operation"
                                type="in"/>
                        </a>
                        <a v-for="operation in exports"
                            :key="operation.id"
                            class="navbar-item">
                            <operation :operation="operation"
                                type="out"/>
                        </a>
                    </div>
                </template>
            </navbar-item>
        </template>
    </core-i-o>
</template>

<script>
import { clickOutside } from '@enso-ui/directives';
import { library } from '@fortawesome/fontawesome-svg-core';
import {
    faSyncAlt, faDatabase, faCaretLeft, faCaretRight,
} from '@fortawesome/free-solid-svg-icons';
import NavbarItem from '@enso-ui/ui/src/bulma/components/navbar/NavbarItem.vue';
import CoreIO from '../../../core/components/navbar/IO.vue';
import Operation from './io/Operation.vue';

library.add(faSyncAlt, faDatabase, faCaretLeft, faCaretRight);

export default {
    name: 'IO',

    directives: { clickOutside },

    components: { CoreIO, Operation, NavbarItem },
};
</script>

<style lang="scss">
    div.operation-list {
        width: 300px;
        overflow-x: hidden;
        max-height: 400px;
        overflow-y: auto;
    }
</style>
