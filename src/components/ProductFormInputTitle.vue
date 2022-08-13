<template>
    <div
        class="product-form-input-title"
        :class="{
            'required': required
        }"
    >
        <span>
            <slot/>
        </span>
    </div>
</template>

<script>
export default {
    name: 'ProductFormInputTitle',
    props: {
        required: {
            type: Boolean,
            required: false,
            default: false
        }
    }
};
</script>

<style lang="scss" scoped>
    .product-form-input-title {
        font-weight: 400;
        font-size: 10px;
        line-height: 13px;
        letter-spacing: -0.02em;
        color: #49485E;
        margin-bottom: 4px;

        span {
            position: relative;
        }
        &.required span::after {
            content: '';
            position: absolute;
            right: -5px;
            top: 0;
            background-image: url('../assets/images/title-required.svg');
            width: 4px;
            height: 4px;
        }
    }
</style>
