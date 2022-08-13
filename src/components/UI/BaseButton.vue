<template>
    <div class="base-button" :class="{ 'base-button__disable': disabled }">
        <button @click="$emit('click')">
            <slot/>
        </button>
    </div>
</template>

<script>
export default {
    props: {
        disabled: {
            type: Boolean,
            default: false
        }
    }
};
</script>


<style lang="scss" scoped>
    .base-button {
        width: 100%;

        button {
            cursor: pointer;
            width: 100%;
            height: 36px;
            font-style: normal;
            font-weight: 600;
            font-size: 12px;
            line-height: 15px;
            text-align: center;
            letter-spacing: -0.02em;
            outline: none;
            border: none;
            border-radius: 10px;
            background: #7BAE73;
            color: #fff;
            box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
        }
        &.base-button__disable {
            button {
                background: #EEEEEE;
                color: #B4B4B4;
                box-shadow: none;
                cursor: default;
            }
        }
    }
</style>
