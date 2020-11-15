<template>
  <div>
    <nav
      id="mobile-nav"
      class="mobile-nav fixed left-0 top-0 h-screen w-full overflow-y-auto pt-12 bg-blue-900 z-50 md:hidden"
      :class="toggleNav ? 'menu-visible': ''"
    >
      <ul>
        <li class="level-1 ml-4 mb-4 md:mr-4 md:mb-0">
          <a href="#" class="ml-4 text-gray-200 hover:text-gray-600" @click="toggleTheme">
            <svg v-if="theme === 'theme-light'" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-moon"><path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/></svg>
            <svg v-else xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-sun"><circle cx="12" cy="12" r="5"/><path d="M12 1v2M12 21v2M4.22 4.22l1.42 1.42M18.36 18.36l1.42 1.42M1 12h2M21 12h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42"/></svg>
          </a>
        </li>
        <li
          class="level-1 mb-4 md:mr-4 md:mb-0"
          v-for="element in $static.metadata.menu"
          :key="element.name"
        >
          <g-link
            :to="element.link"
            class="link block py-2 px-5 text-white text-3xl hover:text-blue-300"
            active-class="is-active-link"
            exact-active-class="active text-blue-300"
          >{{ element.name }}</g-link>
        </li>
      </ul>
    </nav>

    <button
      id="mobile-nav-toggle"
      class="mobile-nav-toggle block fixed h-16 w-full bottom-0 flex items-center justify-center font-bold border-none bg-blue-900 text-white z-50 focus:outline-none md:hidden"
      :class="toggleNav ? 'menu-toggle-active': ''"
      aria-expanded="false"
      aria-controls="mobile-nav"
      @click="toggle"
    >
      <span class="mobile-nav-label mr-2 font-medium">Menu</span>

      <span class="mobile-nav-icon" aria-hidden="true">
        <span class="mobile-nav-icon-line bg-white w-6 block transition mb-1"></span>
        <span class="mobile-nav-icon-line bg-white w-6 block transition mb-1"></span>
        <span class="mobile-nav-icon-line bg-white w-6 block transition"></span>
      </span>
    </button>
  </div>
</template>

<static-query>
query {
  metadata {
    menu {
      name
      link
    }
  }
}
</static-query>

<script>
let myBody = {
  classList : {}
};
export default {
  props: {
    theme: {
      type: String,
      required: true
    }
  },

  data() {
    return {
      toggleNav: false
    }
  },

  methods: {
    toggle() {
      this.toggleNav = !this.toggleNav
    },

    toggleTheme() {
      const newTheme = this.theme === 'theme-light' ? 'theme-dark' : 'theme-light'
      localStorage.setItem('theme', newTheme)
      this.$emit('theme-changed', newTheme)
    }
  }

}
</script>
