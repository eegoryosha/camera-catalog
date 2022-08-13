<template>
    <div id="app">
        <product-catalog/>
    </div>
</template>

<script>
import ProductCatalog from './views/ProductCatalog.vue';

export default {
    name: 'Main',
    components: {
        ProductCatalog,
    },
};
</script>

<style>
    @font-face {
        font-family: 'Source Sans Pro';
        src: url('./assets/fonts/SourceSansPro/SourceSansPro-Regular.ttf') format('ttf');
        font-weight: 400;
        font-style: normal;
        font-display: swap;
    }
    @font-face {
        font-family: 'Source Sans Pro';
        src: url('./assets/fonts/SourceSansPro/SourceSansPro-SemiBold.ttf') format('ttf');
        font-weight: 600;
        font-style: normal;
        font-display: swap;
    }

    /* @font-face {
        font-family: 'Navigo';
        src: url('../fonts/navigo/Navigo-ExtraLight.eot');
        src: url('../fonts/navigo/Navigo-ExtraLight.eot?#iefix') format('embedded-opentype'),
            url('../fonts/navigo/Navigo-ExtraLight.woff2') format('woff2'),
            url('../fonts/navigo/Navigo-ExtraLight.woff') format('woff'),
            url('../fonts/navigo/Navigo-ExtraLight.ttf') format('truetype');
        font-weight: 200;
        font-style: normal;
        font-display: swap;
    }

    @font-face {
        font-family: 'Navigo';
        src: url('../fonts/navigo/Navigo-Black.eot');
        src: url('../fonts/navigo/Navigo-Black.eot?#iefix') format('embedded-opentype'),
            url('../fonts/navigo/Navigo-Black.woff2') format('woff2'),
            url('../fonts/navigo/Navigo-Black.woff') format('woff'),
            url('../fonts/navigo/Navigo-Black.ttf') format('truetype');
        font-weight: 900;
        font-style: normal;
        font-display: swap;
    }

    @font-face {
        font-family: 'Navigo';
        src: url('../fonts/navigo/Navigo-Medium.eot');
        src: url('../fonts/navigo/Navigo-Medium.eot?#iefix') format('embedded-opentype'),
            url('../fonts/navigo/Navigo-Medium.woff2') format('woff2'),
            url('../fonts/navigo/Navigo-Medium.woff') format('woff'),
            url('../fonts/navigo/Navigo-Medium.ttf') format('truetype');
        font-weight: 500;
        font-style: normal;
        font-display: swap;
    }

    @font-face {
        font-family: 'Navigo';
        src: url('../fonts/navigo/Navigo-Light.eot');
        src: url('../fonts/navigo/Navigo-Light.eot?#iefix') format('embedded-opentype'),
            url('../fonts/navigo/Navigo-Light.woff2') format('woff2'),
            url('../fonts/navigo/Navigo-Light.woff') format('woff'),
            url('../fonts/navigo/Navigo-Light.ttf') format('truetype');
        font-weight: 300;
        font-style: normal;
        font-display: swap;
    }

    @font-face {
        font-family: 'Navigo';
        src: url('../fonts/navigo/Navigo-Thin.eot');
        src: url('../fonts/navigo/Navigo-Thin.eot?#iefix') format('embedded-opentype'),
            url('../fonts/navigo/Navigo-Thin.woff2') format('woff2'),
            url('../fonts/navigo/Navigo-Thin.woff') format('woff'),
            url('../fonts/navigo/Navigo-Thin.ttf') format('truetype');
        font-weight: 100;
        font-style: normal;
        font-display: swap;
    }

    @font-face {
        font-family: 'Navigo';
        src: url('../fonts/navigo/Navigo-Regular.eot');
        src: url('../fonts/navigo/Navigo-Regular.eot?#iefix') format('embedded-opentype'),
            url('../fonts/navigo/Navigo-Regular.woff2') format('woff2'),
            url('../fonts/navigo/Navigo-Regular.woff') format('woff'),
            url('../fonts/navigo/Navigo-Regular.ttf') format('truetype');
        font-weight: normal;
        font-style: normal;
        font-display: swap;
    }

    @font-face {
        font-family: 'Navigo';
        src: url('../fonts/navigo/Navigo-Bold.eot');
        src: url('../fonts/navigo/Navigo-Bold.eot?#iefix') format('embedded-opentype'),
            url('../fonts/navigo/Navigo-Bold.woff2') format('woff2'),
            url('../fonts/navigo/Navigo-Bold.woff') format('woff'),
            url('../fonts/navigo/Navigo-Bold.ttf') format('truetype');
        font-weight: bold;
        font-style: normal;
        font-display: swap;
    } */
    body {
        font-family: 'Source Sans Pro';
        background: #FAF9F7;
    }
    * {
        box-sizing: border-box;
    }
</style>
