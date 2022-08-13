<template>
    <transition-group name="result-list" class="products-list">
        <slot/>
    </transition-group>
</template>

<script>

export default {
    name: 'ProductsList',
    components: {

    },
    data() {
        return {

        };
    },
    methods: {

    }

};
</script>

<style lang="scss" scoped>
.products-list {
    max-width: 100%;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 16px;

    @media(max-width: 1099px) {
        grid-template-columns: 1fr 1fr;
    }
    @media(max-width: 767px) {
        grid-template-columns: 1fr;
    }
}
.result-list-enter-active, .list-leave-active {
  transition: all 1s;
}
.result-list-enter, .list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
