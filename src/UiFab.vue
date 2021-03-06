<template>
    <button
        class="ui-fab" :class="[this.type, this.color]" :title="tooltip"
        :aria-label="ariaLabel || tooltip" v-disabled="disabled" v-el:button
    >
        <ui-icon class="ui-fab-icon" :icon="icon"></ui-icon>

        <ui-ripple-ink :trigger="$els.button" v-if="!hideRippleInk && !disabled"></ui-ripple-ink>
    </button>
</template>

<script>
import UiIcon from './UiIcon.vue';

import disabled from './directives/disabled';

import ShowsRippleInk from './mixins/ShowsRippleInk';

export default {
    name: 'ui-fab',

    props: {
        type: {
            type: String,
            default: 'normal',
            coerce(type) {
                return 'ui-fab-' + type;
            }
        },
        color: {
            type: String,
            default: 'default', // 'default', primary', or 'accent'
            coerce(color) {
                return 'color-' + color;
            }
        },
        icon: {
            type: String,
            required: true
        },
        tooltip: String,
        ariaLabel: String,
        disabled: {
            type: Boolean,
            default: false
        }
    },

    components: {
        UiIcon
    },

    mixins: [
        ShowsRippleInk
    ],

    directives: {
        disabled
    }
};
</script>

<style lang="stylus">
@import './styles/imports';

.ui-fab {
    position: relative;
    outline: none;
    border: none;
    z-index: $z-index-fab;

    display: flex;
    align-items: center;
    justify-content: center;

    border-radius: 50%;

    box-shadow: 0 2px 5px 0 alpha(black, 0.2), 0 2px 10px 0 alpha(black, 0.16);
    transition: box-shadow 0.3s ease;

    &:hover:not([disabled]),
    body[modality="keyboard"] &:focus {
        box-shadow: 0 8px 17px 0 alpha(black, 0.25), 0 6px 20px 0 alpha(black, 0.2);
    }

    &.color-default {
        background-color: white;
        color: $md-dark-secondary;

        .ui-fab-icon {
            color: $md-dark-secondary;
        }

        .ui-ripple-ink .ripple.held {
            opacity: 0.2;
        }
    }

    &.color-primary,
    &.color-accent {
        color: white;

        .ui-fab-icon {
            color: white;
        }

        .ui-ripple-ink .ripple.held {
            opacity: 0.7;
        }
    }

    &.color-primary {
        background-color: $md-brand-primary;

        body[modality="keyboard"] &:focus {
            background-color: darken($md-brand-primary, 10%);
        }
    }

    &.color-accent {
        background-color: $md-brand-accent;

        body[modality="keyboard"] &:focus {
            background-color: darken($md-brand-accent, 10%);
        }
    }

    .ui-ripple-ink {
        border-radius: 50%;
    }
}

.ui-fab-normal {
    width: 56px;
    height: 56px;
}

.ui-fab-mini {
    width: 40px;
    height: 40px;
}

.ui-fab-icon {
    margin: 0;
}
</style>
