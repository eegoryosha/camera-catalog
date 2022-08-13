<template>
    <div class="base-input">
        <textarea
            :value="value"
            :name="name"
            :placeholder="placeholder"
            :maxlength="maxLength"
            @input="onInput"
        ></textarea>
    </div>
</template>

<script>

export default {
    name: 'BaseTextarea',
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
        maxLength: {
            type: Number,
            default: 150
        }
    },
    data() {
        return {

        };
    },
    methods: {
        onInput(event) {
            this.$emit('onInput', event.target.value);
        }
    }
};
</script>

<style lang="scss" scoped>
    .base-input {


        textarea {
            width: 100%;
            height: 108px;
            padding: 10px 16px;
            background: #FFFEFB;
            box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
            border-radius: 4px;
            outline: none;
            border: none;
            width: 100%;
            font-size: 12px;
            color: #3F3F3F;
            resize: none;

            &::placeholder {
                font-family: 'Source Sans Pro';
                font-size: 12px;
                color: #B4B4B4;
            }
        }
    }
</style>
