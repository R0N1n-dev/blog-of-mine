<template>
  <IContainer>
    <h1>Blog</h1>
    <IRow>
      <IColumn
        v-for="{ _path: slug, title, description, cover } in blogPosts"
        :key="slug"
      >
        <ICard>
          <template #image>
            <img :src="cover" alt="Card Image" />
          </template>
          <h2>{{ title }}</h2>
          <p>
            {{ description }}
          </p>
          <NuxtLink :to="slug">Read</NuxtLink>
        </ICard>
      </IColumn>
    </IRow>
  </IContainer>
</template>

<script setup>
/*const blogPosts = await queryContent("/articles")
  .sort({ date: -1 }) // show latest articles first
  .where({ _partial: false }) // exclude the Partial files
  .find();*/
const { data: blogPosts } = await useAsyncData("blogPosts", () =>
  queryContent("/articles").find()
);
</script>
