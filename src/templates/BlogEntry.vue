<template>
  <Layout>
    <section id="container-centre" class="column centre flex-1">
      <div class="post-header mb-12 md:mb-20">
        <h1
          class="page-title text-3xl md:text-center md:text-5xl lg:text-6xl"
          v-html="$page.blog.title"
        ></h1>
        <div class="text-sm md:text-base text-gray-600 flex justify-center">
          <p class="author">{{ $page.blog.author.name }}</p>
          <figure v-if="$page.blog.author.image">
            <g-image
              class="rounded-full loaded"
              alt="profile picture"
              :src="$page.blog.author.image"
            />
          </figure>
          <p class="px-2">—</p>
          <time :datetime="$page.blog.datetime">{{ $page.blog.humanTime }}</time>
          <p class="px-2">—</p>
          <p class="category">
            Posted in
            <g-link :to="$page.blog.category.path">{{ $page.blog.category.title }}</g-link>
          </p>
        </div>
        <figure v-if="$page.blog.image" class="mt-10 md:mt-20">
          <g-image :alt="$page.blog.image_caption" :src="$page.blog.image" />
          <figcaption
            class="text-center text-sm italic text-gray-600 mt-4"
          >{{ $page.blog.image_caption }}</figcaption>
        </figure>
      </div>

      <div class="content post md:px-16">
        <p v-if="$page.blog.excerpt" v-html="$page.blog.excerpt"></p>
        <div v-html="$page.blog.content"></div>
        <ul class="flex pt-8 border-t border-gray-100">
          <li class="mr-2" v-for="tag in $page.blog.tags" :key="tag.id">
            <g-link
              :to="tag.path"
              class="rounded py-1 px-2 text-blue-900 bg-transparent border border-blue-900 hover:border-transparent hover:bg-blue-900 hover:text-blue-300"
            >{{ tag.title}}</g-link>
          </li>
        </ul>
      </div>

    </section>
  </Layout>
</template>

<script>
  export default {
    metaInfo() {
      return {
        title: this.$page.blog.title,
        meta: [
          {
            key: 'description',
            name: 'description',
            content: this.$page.blog.excerpt
          },
          {
            key: 'keywords',
            name: 'keywords',
            content: 'web developer, tech blog, adam bailey, software developer'
          }
        ]
      };
    }
  };
</script>

<page-query>
  query($id: ID!) {
    blog(id: $id, orderBy: {field: created, direction: ASC}) {
      title
      path
      image(width:1200)
      image_caption
      excerpt
      content
      humanTime : created(format:"Do MMMM YYYY")
      datetime : created(format:"ddd MMM DD YYYY hh:mm:ss zZ")
      category {
        title
        path
      }
      author {
        name
        image(width:20)
      }
      tags {
        id
        title
        path
      }
    }
  }
</page-query>
