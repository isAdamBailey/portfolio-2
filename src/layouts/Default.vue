<template>
  <div class="content-wrapper bg-background-primary text-copy-primary leading-normal text-lg" :class="theme">
    <a class="visually-hidden" href="#main">Skip to content</a>

    <div id="wrapper" class="wrapper pb-16 md:pb-0 flex flex-col relative min-h-screen">

      <Header
          :theme="theme"
          @theme-changed="onChangeTheme"
      />

      <main id="main" class="main inner flex flex-1 flex-col py-10 lg:py-20">
        <slot/>
      </main>

      <Footer/>

    </div>

    <ClientOnly>
      <ResponsiveNav/>
    </ClientOnly>

  </div>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<script>
import Header from '~/layouts/partials/Header.vue'
import Footer from '~/layouts/partials/Footer.vue'
import ResponsiveNav from '~/layouts/partials/ResponsiveNav.vue'

export default {
  components: {
    Header,
    Footer,
    ResponsiveNav
  },

  data() {
    return {
      theme: ''
    };
  },

  created() {
    if (process.isClient) {
      this.theme = localStorage.getItem('theme') || 'theme-light'
    }
  },

  mounted() {
    if (window.netlifyIdentity) {
      window.netlifyIdentity.on("init", user => {
        if (!user) {
          window.netlifyIdentity.on("login", () => {
            document.location.href = "/admin/";
          });
        }
      });
    }
  },

  methods: {
    onChangeTheme(event) {
      this.theme = event;
    }
  }
}
</script>
