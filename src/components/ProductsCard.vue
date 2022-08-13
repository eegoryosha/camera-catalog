<template>
    <div class="products-card">
        <remove-button class="products-card__remove-button" @click="removeProduct"></remove-button>

        <img :src="product.image">
        <div class="products-card__info">
            <div class="products-card__body">
                <div class="products-card__title">
                    <span>{{ product.name }}</span>
                </div>
                <div class="products-card__description">
                    <span>{{ product.description }}</span>
                </div>
            </div>

            <div class="products-card__price">{{ modifyPrice }} ₽</div>
        </div>
    </div>
</template>

<script>
import RemoveButton from './UI/RemoveButton.vue';
export default {
    name: 'ProductsList',
    components: {
        RemoveButton
    },
    props: {
        product: {
            type: Object,
            required: true
        }
    },
    methods: {
        removeProduct() {
            this.$emit('removeProduct', this.product);
        }
    },
    computed: {
        modifyPrice() {
            return new Intl.NumberFormat('ru-RU').format(this.product.price ?? 0);
        }
    }
};
</script>

<style lang="scss" scoped>
.products-card {
    max-width: 100%;
    min-width: 100%;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    display: flex;
    flex-direction: column;
    position: relative;

    &__body {
        overflow: hidden;
    }
    &__remove-button {
        position: absolute;
        right: -10px;
        top: -10px;
        display: none;
    }
    &:hover &__remove-button {
        display: block;
    }
    &__info {
        padding: 16px 16px 24px;
        flex-grow: 1;

        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }
    &__title {
        font-weight: 600;
        font-size: 20px;
        line-height: 25px;
        color: #3F3F3F;
        margin-bottom: 16px;
    }
    &__description {
        font-size: 16px;
        line-height: 20px;
        color: #3F3F3F;
        margin-bottom: 32px;
    }
    &__price {
        font-weight: 600;
        font-size: 24px;
        line-height: 30px;
        color: #3F3F3F;
    }
    img {
        max-width: 100%;
        width: 100%;
        height: 200px;
        object-fit: cover;
        border-radius: 4px 4px 0 0;
    }
}
</style>
