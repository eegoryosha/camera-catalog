<template>
    <div class="product-add-form">
        <div class="product-add-form__controls">
            <div class="form-control" :class="{ 'error': nameErrors.length }">
                <product-form-input-title :required="true">Наименование товара</product-form-input-title>
                <base-input :maxLength="25" :error="nameErrors.length != 0" :value="product.name" placeholder="Введите наименование товара" @onInput="onInputName" />
                <div class="form-control__error" v-if="nameErrors.length">{{ nameErrors[0] }}</div>
            </div>

            <div class="form-control">
                <product-form-input-title>Описание товара</product-form-input-title>
                <base-textarea :value="product.description" placeholder="Введите описание товара" @onInput="onInputDescription" />
            </div>

            <div class="form-control" :class="{ 'error': imageErrors.length }">
                <product-form-input-title :required="true">Ссылка на изображение товара</product-form-input-title>
                <base-input :error="imageErrors.length != 0" :value="product.image" placeholder="Введите ссылку" @onInput="onInputImage" />
                <div class="form-control__error" v-if="imageErrors.length">{{ imageErrors[0] }}</div>
            </div>

            <div class="form-control">
                <product-form-input-title :required="true">Цена товара</product-form-input-title>
                <base-input :maxLength="12" :callback="validLetters" :error="priceErrors.length != 0" :value="product.price" placeholder="Введите цену" @onInput="onInputPrice" />
                <div class="form-control__error" v-if="priceErrors.length">{{ priceErrors[0] }}</div>
            </div>
        </div>

        <base-button :disabled="$v.$invalid" @click="addProduct">Добавить товар</base-button>
    </div>
</template>

<script>
import BaseButton from '@/components/UI/BaseButton';
import BaseInput from '@/components/UI/BaseInput.vue';
import BaseTextarea from '@/components/UI/BaseTextarea.vue';
import ProductFormInputTitle from '@/components/ProductFormInputTitle';
import { validationMixin } from 'vuelidate';
import { required } from 'vuelidate/lib/validators';

export default {
    name: 'ProductAddForm',
    components: {
        BaseInput, BaseTextarea, ProductFormInputTitle, BaseButton
    },
    mixins: [validationMixin],
    data() {
        return {
            product: {
                name: '',
                description: '',
                image: '',
                price: '',
                id: null
            }
        };
    },
    methods: {
        onInputName(value) {
            this.product.name = value;
            this.$v.product.name.$touch();
        },
        onInputDescription(value) {
            this.product.description = value;
            this.$v.product.description.$touch();
        },
        onInputImage(value) {
            this.product.image = value;
            this.$v.product.image.$touch();
        },
        onInputPrice(value) {
            this.product.price = value;
            this.$v.product.price.$touch();
        },
        addProduct() {
            if (this.$v.$invalid) return;

            this.product.id = Math.round(new Date().getTime() + Math.random() * 100);
            this.$emit('addProduct', this.product);


            this.product = {
                name: '',
                description: '',
                image: '',
                price: '',
                id: null
            };
            this.$v.$reset();
        },
        validLetters(event) {
            const input = event.target;
            const value = input.value;

            const num = Number(value.replace(/\D+/g, ''));

            if (num === 0) {
                input.value = '';
            } else {
                input.value = new Intl.NumberFormat('ru-RU').format(num);
            }
        },
    },
    computed: {

        nameErrors() {
            const errors = [];

            if (!this.$v.product.name.$dirty) return errors;
            if (!this.$v.product.name.required) errors.push('Поле является обязательным');

            return errors;
        },
        imageErrors() {
            const errors = [];

            if (!this.$v.product.image.$dirty) return errors;
            if (!this.$v.product.image.required) errors.push('Поле является обязательным');

            return errors;
        },
        priceErrors() {
            const errors = [];

            if (!this.$v.product.price.$dirty) return errors;
            if (!this.$v.product.price.required) errors.push('Поле является обязательным');

            return errors;
        }
    },
    validations: {
        product: {
            name: {
                required
            },
            description: {},
            image: {
                required,
            },
            price: {
                required,
            }
        }
    }

};
</script>

<style lang="scss" scoped>
    .product-add-form {
        width: 100%;
        background: #FFFEFB;
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        border-radius: 4px;
        padding: 24px;

        &__controls {
            margin-bottom: 24px;
        }
    }

    .form-control {
        margin-bottom: 16px;
        position: relative;



        &__error {
            position: absolute;
            bottom: -14px;
            font-size: 8px;
            line-height: 10px;
            letter-spacing: -0.02em;
            color: #FF8484;
        }
    }
</style>
