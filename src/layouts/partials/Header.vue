<template>
  <header
    id="header"
    class="header bg-blue-900 flex flex-col md:flex-row md:justify-between items-center p-4 md:p-6"
    role="banner"
  >
    <div class="flex justify-between w-full items-center">
      <g-link
          class="text-white font-bold text-2xl md:text-3xl hover:text-gray-600"
          to="/"
          aria-label="Back to home"
      >{{ $static.metadata.siteName }}</g-link>

      <a href="#" class="text-gray-200 hover:text-gray-600 md:mr-10" @click="toggleTheme">
        <svg v-if="theme === 'theme-light'" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-moon"><path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/></svg>
        <svg v-else xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-sun"><circle cx="12" cy="12" r="5"/><path d="M12 1v2M12 21v2M4.22 4.22l1.42 1.42M18.36 18.36l1.42 1.42M1 12h2M21 12h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42"/></svg>
      </a>
    </div>

    <nav id="nav" class="nav hidden md:flex">
      <ul class="menu flex flex-col md:flex-row items-center list-reset text-base">
        <li
          class="level-1 mb-4 md:mr-4 md:mb-0"
          v-for="element in $static.metadata.menu"
          :key="element.name"
        >
          <g-link
            :to="element.link"
            class="link font-bold text-white hover:text-blue-300"
            active-class="is-active-link"
            exact-active-class="active text-blue-300"
          >{{ element.name }}</g-link>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  props: {
    theme: {
      type: String,
      required: true
    }
  },

  methods: {
    socialIcon(element) {
      return `/icons.svg#icon-${element.icon}`;
    },
    toggleTheme() {
      const newTheme = this.theme === 'theme-light' ? 'theme-dark' : 'theme-light'
      localStorage.setItem('theme', newTheme)
      this.$emit('theme-changed', newTheme)
    }
  }
};
</script>

<static-query>
query {
  metadata {
    siteName
    menu {
      name
      link
    }
  }
}
</static-query>
