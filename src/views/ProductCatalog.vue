<template>
    <div class="container">
        <div class="product-catalog">
            <div class="product-catalog__form">
                <div class="product-catalog__header">
                    <product-form-title>Добавление товара</product-form-title>
                </div>
                <div class="product-catalog__body">
                    <product-add-form  @addProduct="addProduct"/>
                </div>
            </div>
            <div class="product-catalog__list">
                <div class="product-catalog__header">
                    <div class="product-catalog__filter">
                        <base-select
                            :options="[{ value: 'default', name: 'По наименованию' }, { value: 'ascending', name: 'По возрастанию' }, { value: 'descending', name: 'По убыванию' }]"
                            @change="sortProducts"
                        />
                    </div>
                </div>
                <div class="product-catalog__body">
                    <transition-group name="result-list" class="products-list">
                        <products-card
                            v-for="product in sortedProducts"
                            :key="product.id"
                            :product="product"
                            @removeProduct="removeProduct"
                        />
                    </transition-group>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import  ProductAddForm from '@/components/ProductAddForm.vue';
import ProductFormTitle from '@/components/ProductFormTitle.vue';
import BaseSelect from '@/components/UI/BaseSelect.vue';
import ProductsCard from '../components/ProductsCard.vue';
import products from '@/data/products';

export default {
    name: 'ProductCatalog',
    components: {
        ProductAddForm,
        ProductFormTitle,
        BaseSelect,
        ProductsCard
    },
    data() {
        return {
            products: null,
            sortedType: 'default'
        };
    },
    methods: {
        addProduct({ id, name, description, image, price }) {
            this.products.push({
                id,
                name,
                description,
                image,
                price: Number(price.replace(/\D+/g, ''))
            });

            this.saveProductsToLocalstorage();
        },
        removeProduct(product) {
            this.products = this.products.filter(el => el.id != product.id);

            this.saveProductsToLocalstorage();
        },
        sortProducts(type) {
            this.sortedType = type;
        },
        saveProductsToLocalstorage() {
            localStorage.setItem('PRODUCTS_LIST', JSON.stringify(this.products));
        }
    },
    created() {
        const localStorageProducts = localStorage.getItem('PRODUCTS_LIST');

        this.products = localStorageProducts ? JSON.parse(localStorageProducts) : products;
    },
    computed: {
        sortedProducts() {
            if (this.sortedType == 'ascending') {
                return [...this.products].sort((a, b) => a.price - b.price);
            }
            if (this.sortedType == 'descending') {
                return [...this.products].sort((a, b) => b.price - a.price);
            }
            return [...this.products].sort((a, b) => a.name.localeCompare(b.name));
        }
    }
};
</script>

<style lang="scss" scoped>
.container {
    max-width: 1396px;
    padding: 0 10px;
    width: 100%;
    margin: 0 auto;
}
.product-catalog {
    display: flex;
    justify-content: space-between;

    @media(max-width: 600px) {
        flex-direction: column;
        justify-content: flex-start;
    }

    &__form {
        min-width: 332px;
        margin-right: 16px;

        @media(max-width: 1099px) {
            min-width: 310px;
        }
        @media(max-width: 600px) {
            margin-bottom: 32px;
            width: 100%;
        }
        @media(max-width: 600px) {
            min-width: 100%;
        }
    }
    &__list {
        width: 100%;
    }
    &__header {
        height: 36px;
        margin-bottom: 16px;
    }
    &__filter {
        display: flex;
        justify-content: flex-end;
    }
}

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
  transition: all 0.8s ease-in-out;
}
.result-list-enter, .list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
.result-list-move {
    transition: transform 0.4s ease-in-out;
}

</style>
