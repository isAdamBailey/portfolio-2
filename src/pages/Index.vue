<template>
  <Layout>
    <section id="container-center" class="column center flex-1">
      <h1 class="page-title">Hi! I'm Adam Bailey</h1>
      <div class="content">
        <p>
          I'm an experienced Software Developer working primarily in
          <a href="https://laravel.com/">Laravel</a> and
          <a href="https://vuejs.org/">Vue.js</a>.
        </p>

        <div class="flex justify-center">
          <a href="https://drive.google.com/open?id=1uPXrHJ42H8d4Um-2cXLfA2e7t32GZFI6">
            <button class="rounded py-4 px-6 text-white font-bold bg-pink-500 hover:bg-pink-600 mb-12">
              Open My Resume!
            </button>
          </a>
        </div>

        <div class="page-title mt-12">Projects</div>
        <p class="text-gray-700">While most of my best work was done in private repositories, Here are some examples
          of open source projects ive worked on.</p>
        <div
          v-for="project in projects"
          class="max-w-sm w-full lg:max-w-full lg:flex mb-4 shadow-lg"
        >
          <div class="border-r border-b border-l border-t border-gray-300 bg-white rounded p-4 flex flex-col justify-between">
            <div>
              <div class="text-gray-900 font-bold text-3xl">{{ project.title }}</div>
              <p class="text-gray-700 text-base">{{ project.description }}</p>
            </div>
            <div class="flex justify-center inline-flex h-12">
              <a :href="project.siteLink">
                <button class="rounded-l py-2 px-4 w-40 text-white font-bold bg-pink-500 hover:bg-pink-600">
                  Live Site
                </button>
              </a>
              <a :href="project.github">
                <button class="rounded-r py-2 px-4 w-40 text-white font-bold bg-pink-500 hover:bg-pink-600">
                  Github
                </button>
              </a>
            </div>
          </div>
        </div>

      </div>
    </section>
  </Layout>
</template>

<script>
export default {
  metaInfo: {
    title: "Home"
  },
  data() {
    return {
      projects: [
        {
          title: 'This Portfolio',
          description: `Yes, that's right, the site you're on right now is an experiment in learning static site
          generation and GraphQL. It is made with Tailwindcss, Gridsome, VueJs, and uses Forestry.io for a backend CMS.`,
          siteLink: '/',
          github: 'https://github.com/Owlnofeathers/portfolio-2'
        },
        {
          title: 'Gif Search Tool',
          description: `I was on a team who made sprint planning documents with silly names and a related gif.
          This site allows you to search for gifs and several word combinations using the giphy api and the datamuse
          api. The site is built in VueJs and deployed on netlify.com`,
          siteLink: 'https://gif-search-tool.netlify.com/',
          github: 'https://github.com/Owlnofeathers/gif-search-tool'
        },
        {
          title: 'Family History',
          description: `I used PHP, jQuery, and BootStrap with LightBox and Masonry plugins to display my family's
          local history. It features a full back end dashboard, so historical images and stories can be managed by
          authenticated users, and is fully responsive.`,
          siteLink: 'https://hansennorthforkranch.ajamesb.com/',
          github: 'https://github.com/Owlnofeathers/hansennorthforkranch.ajamesb.com'
        },
        {
          title: 'Record Collection',
          description: `This site is built on Laravel and VueJs, Pulling in the Discogs API to review my
          record collection. It has the ability to add records to the database from the Discogs api with one click.
          The site is fully responsive with Bootstrap 3.`,
          siteLink: 'https://records.ajamesb.com/',
          github: 'https://github.com/Owlnofeathers/vinyl-database'
        },
        {
          title: 'Doctor\'s Office',
          description: `A basic bootstrap site built in PHP, for a clinical psychologist's office. I worked with the
          client to meet the needs of his office while incorporating his hobby of photography.`,
          siteLink: 'https://albernstein.com/',
          github: 'https://github.com/Owlnofeathers/albernstein.com'
        }
      ]
    };
  }
};
</script>
