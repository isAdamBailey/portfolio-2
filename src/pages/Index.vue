<template>
  <Layout>
    <section id="container-center" class="column center flex-1">
      <h1 class="page-title">Hi! I'm Adam Bailey</h1>
      <div class="content">
        <p>
          I'm a Software Developer experienced in
          <TypingText :words="['Laravel.', 'PHP.', 'Javascript.', 'Vue.']"/>
        </p>

        <div class="flex justify-center">
          <a href="https://drive.google.com/open?id=1uPXrHJ42H8d4Um-2cXLfA2e7t32GZFI6">
            <button>Open My Resume!</button>
          </a>
        </div>

        <div class="page-title mt-12">Projects</div>
        <p class="text-copy-primary">While most of my best work was done in private repositories, Here are some examples
          of open source projects ive worked on.</p>
        <div class="posts flex justify-center flex-wrap">
          <div
            v-for="project in $static.metadata.projects"
            class="flex flex-col justify-between max-w-md rounded overflow-hidden shadow-lg m-4 bg-background-card"
          >
            <div class="p-4">
              <div class="text-copy-heading font-bold text-3xl">{{ project.title }}</div>
              <p class="text-copy-primary text-base">{{ project.description }}</p>
            </div>
            <div class="justify-around inline-flex pb-4">
              <a :href="project.siteLink">
                <button>Live Site</button>
              </a>
              <a :href="project.github">
                <button>Github</button>
              </a>
            </div>
          </div>
        </div>

      </div>
    </section>
  </Layout>
</template>

<script>
import TypingText from '../layouts/partials/TypingText'

export default {
  components: { TypingText },
  metaInfo: {
    title: "Home"
  },
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
