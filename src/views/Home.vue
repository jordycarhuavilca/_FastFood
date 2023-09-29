<template>
  <div class="annou" id="annou" v-if="isActive">
    <div class="annou__content">
      <img
        class="annou__icon3dFrench-fries"
        src="https://raw.githubusercontent.com/jordycarhuavilca/fast-food/master/img/icon-food/french_fries.png"
        alt=""
      />
      <p class="annou__text d-none d-md-block">
        ¿Nuevo en Fast Food? Disfuta de...
      </p>
      <span class="annou__text-span">¡Entrega gratis por 30 dias!</span>
      <a href="./html/Login-ux-design.html h1 text-sm" class="btn-Registar"
        >Registrarme</a
      >
      <a
        href="./html/Condiciones.html"
        class="annou__text-terms d-none d-md-block"
        >Terminos y condiciones</a
      >
      <i
        @click="isActive = !isActive"
        class="bx bxs-x-circle"
        style="
          color: rgba(222, 213, 213, 0.5);
          font-size: 1.5rem;
          cursor: pointer;
        "
      ></i>
    </div>
  </div>
  <div>
    <Banner />
  </div>
  <main>
    <div
      class="my-4 d-flex justify-content-center align-items-center d-sm-block"
    >
      <p class="h4 ms-sm-5 pt-3 pb-3">Top restaurantes cerca de ti</p>
    </div>
    <div class="ps-4">
      <swiper
        class="ps-5 pe-5 d-flex justify-content-center align-items-center"
        :modules="modules"
        :slides-per-view="10"
        :spaceBetween="1"
        :breakpoints="{
          '@0.00': {
            slidesPerView: 2,
            spaceBetween: 1,
          },
          '@0.60': {
            slidesPerView: 2,
            spaceBetween: 1,
          },

          '@0.75': {
            slidesPerView: 3,
            spaceBetween: 1,
          },
          '@0.95': {
            slidesPerView: 4,
            spaceBetween: 1,
          },
          '@1.10': {
            slidesPerView: 5,
            spaceBetween: 1,
          },
          '@1.30': {
            slidesPerView: 6,
            spaceBetween: 1,
          },
          '@1.65': {
            slidesPerView: 8,
            spaceBetween: 1,
          },
          '@2.00': {
            slidesPerView: 10,
            spaceBetween: 1,
          },
        }"
        @breakpoint="adjustSize"
        navigation
        @swiper="onSwiper"
        @slideChange="onSlideChange"
      >
        <swiper-slide class="m-0 pl-5">
          <figure :class="isMaxSize ? 'image is-96x96' : 'image is-128x128'">
            <img
              class="rounded"
              src="https://bulma.io/images/placeholders/128x128.png"
            />
          </figure>
        </swiper-slide>
        <swiper-slide v-for="index in 12" :key="index">
          <figure :class="isMaxSize ? 'image is-96x96' : 'image is-128x128'">
            <img
              class="rounded"
              src="https://bulma.io/images/placeholders/128x128.png"
            />
          </figure>
        </swiper-slide>
      </swiper>
    </div>
  </main>

  <div class="pb-5 pt-5">
    <div
      class="my-4 d-flex justify-content-center align-items-center d-sm-block"
    >
      <p class="h4 ms-sm-5 pt-3 pb-3">Top mercados cerca de ti</p>
    </div>
    <Splide
      :options="splideOptions"
      aria-label="My Favorite Images"
      class="ps-5 px-5"
    >
      <SplideSlide
        v-for="({ image, razonSocial }, index) in markets"
        :key="index"
      >
        <div
          class="d-flex flex-row justify-content-center gap-2 align-items-center"
        >
          <figure class="image is-64x64">
            <img class="rounded" :src="image" :alt="razonSocial" />
          </figure>
          <div>
            <span style="font-size: 0.8rem">{{ razonSocial }}</span>
          </div>
        </div>
      </SplideSlide>
    </Splide>
  </div>
  <Footer />
</template>

<script>
import Banner from "../components/Banner.vue";
import { Navigation, Pagination, Scrollbar, A11y } from "swiper/modules";
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";
import Footer from "../components/Footer.vue";
import { Grid } from "@splidejs/splide-extension-grid";
import { Splide, SplideSlide } from "@splidejs/vue-splide";
import { ref } from "vue";
export default {
  name: "Home",
  components: {
    Banner,
    Swiper,
    SwiperSlide,
    Footer,
    Splide,
    SplideSlide,
  },
  data() {
    return {
      isActive: false,
      markets: [
        {
          numImg: 0,
          image:
            "https://images.rappi.pe/marketplace/store_type_1692726265362.png",
          razonSocial: "Holi",
        },
        {
          numImg: 1,
          image:
            "https://images.rappi.pe/marketplace/store_type_1692726530893.png",
          razonSocial: "Flora & Fauna",
        },
        {
          numImg: 2,
          image:
            "https://images.rappi.pe/marketplace/store_type_1686329283463.png",
          razonSocial: "La Cesta",
        },
        {
          numImg: 3,
          image:
            "https://images.rappi.pe/marketplace/store_type_1692726517774.png",
          razonSocial: "Spid",
        },
        {
          numImg: 4,
          image:
            "https://images.rappi.pe/marketplace/store_type_1692715407645.png",
          razonSocial: "Wong",
        },
        {
          numImg: 5,
          image:
            "https://images.rappi.pe/marketplace/store_type_1692726100440.png",
          razonSocial: "Metro",
        },
        {
          numImg: 6,
          image:
            "https://images.rappi.pe/marketplace/almeco_mt_nc-1665068053665.jpeg",
          razonSocial: "Almeco",
        },
        {
          numImg: 7,
          image:
            "https://images.rappi.pe/marketplace/freshmart_mt_nc-1691425932787.jpeg",
          razonSocial: "Freshmart",
        },
      ],
    };
  },
  methods: {
    adjustSize(breakpoint) {
      if (breakpoint.currentBreakpoint === "@0.00") this.isMaxSize = true;
      else this.isMaxSize = false
    },
  },
  setup() {
    const splideOptions = {
      rewind: true,
      type: "slide",
      start: 0,
      perPage: 2,
      gap: "1em",
      arrows: false,
      pagination: false,
      mediaQuery: "min",
      breakpoints: {
        1048: {
          perPage: 6,
        },
        600: {
          perPage: 4,
        },
        500: {
          perPage: 3,
        },
      },
    };
    const isMaxSize = ref(true);
    const onSwiper = (swiper) => {
      console.log(swiper);
    };
    const onSlideChange = () => {
      console.log("slide change");
    };
    return {
      isMaxSize,
      splideOptions,
      onSwiper,
      onSlideChange,
      modules: [Navigation, Pagination, Scrollbar, A11y],
    };
  },
};
</script>

<style>
@import "../assets/announce.css";
@import "bulma/css/bulma.css";
@import "@splidejs/vue-splide/css/core";
</style>
