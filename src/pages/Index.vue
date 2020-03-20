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
        <div class="posts flex justify-center flex-wrap">
          <div
            v-for="project in $static.metadata.projects"
            class="flex flex-col justify-between max-w-md rounded overflow-hidden shadow-lg m-4"
          >
            <div class="p-4">
              <div class="text-gray-900 font-bold text-3xl">{{ project.title }}</div>
              <p class="text-gray-700 text-base">{{ project.description }}</p>
            </div>
            <div class="justify-center inline-flex pb-4">
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
  }
};
</script>

<static-query>
  query {
    metadata {
      projects {
        title
        description
        siteLink
        github
      }
    }
  }
</static-query>
