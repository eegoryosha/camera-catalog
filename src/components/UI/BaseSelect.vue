<template>
    <div class="select" :class="{ 'select__active': isShowDropdown }" ref="parent">
        <div class="select__header" @click="changeDropdown(!isShowDropdown)">
            <input
                :value="selectedValueName"
                ref="input"
                type="text"
                class="select__result"
                readonly
            />
        </div>
        <div class="select__body" v-if="isShowDropdown">
            <div
                class="select__item"
                v-for="option in options"
                :key="option.value"
                @click="changeOption(option.value)"
            >
                {{ option.name }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'BaseSelect',
    props: {
        options: {
            type: Array,
            default: () => [],
        },
    },
    data() {
        return {
            isShowDropdown: false,
            selectedValue: null,
        };
    },
    methods: {
        changeOption(value) {
            this.selectedValue = value;

            this.changeDropdown(false);

            this.$emit('change', value);
        },
        changeDropdown(value) {
            this.isShowDropdown = value;
        },
    },
    computed: {
        selectedValueName() {
            return this.options.find(el => el.value == this.selectedValue).name;
        }
    },
    created() {
        this.selectedValue = this.options[0]?.value ?? null;

        document.addEventListener('click', (e) => {
            if (!this.$el.contains(e.target)) {
                this.changeDropdown(false);
            }
        });
    }
};
</script>

<style lang="scss" scoped>
.select {
    position: relative;
    border-radius: 6px;
    font-weight: 400;
    font-size: 12px;
    line-height: 18px;
    display: flex;
    align-items: center;
    color: #96a3aa;
    input {
        padding: 10px 27px 10px 16px;
        width: 100%;
        font-weight: 400;
        font-size: 12px;
        line-height: 15px;
        color: #b4b4b4;
    }
    &__header {
        background: #fffefb;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;
        display: flex;
        align-items: center;
        cursor: pointer;
        height: 36px;
        position: relative;
        width: 100%;

        &:after {
            content: "";
            position: absolute;
            top: 12px;
            right: 11px;
            width: 6px;
            height: 6px;
            border-top: 1px solid #b4b4b4;
            border-left: 1px solid #b4b4b4;
            transform: rotate(-135deg);
            transition: transform 0.5s cubic-bezier(0.785, 0.135, 0.15, 0.86);
        }
    }
    &__body {
        background: #fffefb;
        position: absolute;
        margin-top: -5px;
        width: 100%;
        z-index: 100;
        max-height: 300px;
        overflow: auto;
        overflow-x: hidden;
        top: 40px;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);

        &::-webkit-scrollbar {
            width: 8px;
        }
        &::-webkit-scrollbar-track {
            background-color: rgb(247, 247, 247);
        }
        &::-webkit-scrollbar-thumb {
            background-color: #cdcdcd;
            border-radius: 4px;
        }
    }
    &__title {
        padding-top: 0px;
        padding-left: 12px;
        position: absolute;
        z-index: 55;
        transition: 0.2s;
        left: 0px;
        top: 50%;
        transform: translate(0, -50%);
        font-size: 16px;
    }
    &__result {
        border: none;
        cursor: pointer;
    }
    &__item {
        padding: 8px;
        cursor: pointer;
        transition: 0.3s;
        &:hover {
            background: #27de70;
            color: #fff;
        }
    }
    &__active .select__body {
        display: block;
    }
    &__active .select__title {
        font-size: 10px;
        top: 0;
        left: 0;
        transform: translate(0, 0);
        line-height: 24px;
    }
    &__selected .select__title {
        font-size: 10px;
        top: 0;
        left: 0;
        transform: translate(0, 0);
        line-height: 24px;
    }
    &:hover &__body {
        border-color: #27de70;
        transition: 0.2s;
    }
    &:hover &__header {
        border-color: #27de70;
        transition: 0.2s;
    }
}
.select.disabled {
    .select__header {
        border: none;
    }
}
.select.select__active {
    .select__header {
        &:after {
            content: "";
            transform: rotate(45deg) translate3d(2px, 2px, 0);
        }
    }
}
input:focus-visible {
    outline: none;
}
@media (max-width: 600px) {
    .select {
        min-width: 143px;
    }
}
@media (max-width: 412px) {
    .fontSize {
        font-size: 13px !important;
    }
}
</style>
