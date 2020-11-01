<template>
  <Layout>
    <section id="container-center" class="column center flex-1">
      <h1 class="page-title">Hi! I'm Adam Bailey</h1>
      <div class="content">
        <p>
          I'm a Software Developer experienced in <span id="swap-text"></span>
        </p>

        <div class="flex justify-center">
          <a href="https://drive.google.com/open?id=1uPXrHJ42H8d4Um-2cXLfA2e7t32GZFI6">
            <button>Open My Resume!</button>
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
class SwappableHeading {
  constructor(element, headings = []) {
    this.element = element;
    this.headings = headings;
    this.current = 1;
  }

  async swap() {
    while (true) {
      await this.wait(1000);

      await this.clear();

      await this.type(this.nextHeading());
    }
  }

  async type(text) {
    while (text.length) {
      await this.append(text[0]);

      text = text.substring(1);
    }
  }

  text() {
    return this.element.innerHTML;
  }

  append(text) {
    this.element.innerHTML += text;

    return this.wait(100);
  }

  async clear() {
    while (this.length()) {
      await this.backspace();
    }
  }

  backspace() {
    this.element.innerHTML = this.text().slice(0, -1);

    return this.wait(100);
  }

  nextHeading() {
    let heading = this.headings[this.current - 1];

    this.increment();

    return heading;
  }

  length() {
    return this.text().length;
  }

  increment() {
    this.current++;

    if (this.current > this.headings.length) {
      this.current = 1;
    }
  }

  async wait(milliseconds) {
    return new Promise(resolve => {
      setTimeout(resolve, milliseconds);
    });
  }
}

export default {
  metaInfo: {
    title: "Home"
  },

  data() {
    return {
      headings: ['Laravel.', 'PHP.', 'Javascript.', 'Vue.']
    };
  },

  mounted() {
    new SwappableHeading(document.getElementById('swap-text'), this.headings).swap();
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

<style lang="scss" scoped>
#swap-text {
  font-weight: bold;
  font-size: 2rem;
}
</style>
