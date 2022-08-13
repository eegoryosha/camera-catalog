<template>
    <div class="base-input">
        <input
            type="text"
            :value="value"
            :name="name"
            :placeholder="placeholder"
            :class="{'base-input__error': error}"
            :maxlength="maxLength"
            @input="onInput"
        >
    </div>
</template>

<script>
export default {
    name: 'BaseInput',
    props: {
        value: {
            type: String,
            default: ''
        },
        name: {
            type: String,
            default: ''
        },
        placeholder: {
            type: String,
            default: ''
        },
        error: {
            type: Boolean,
            default: false
        },
        maxLength: {
            type: [Number,String],
            default: ''
        },
        callback: {
            type: Function,
            default: () => null
        }
    },
    data() {
        return {

        };
    },
    methods: {
        onInput(event) {
            this.callback(event);

            this.$emit('onInput', event.target.value);
        }
    }
};
</script>

<style lang="scss" scoped>
    .base-input {
        width: 100%;

        input {
            width: 100%;
            height: 36px;
            padding: 10px 16px;
            background: #FFFEFB;
            box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
            border-radius: 4px;
            outline: none;
            border: none;
            font-size: 12px;
            color: #3F3F3F;

            &::placeholder {
                font-family: 'Source Sans Pro';
                font-size: 12px;
                color: #B4B4B4;
            }

            &.base-input__error {
                border: 1px solid #FF8484;
                box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
            }
        }

    }
</style>
