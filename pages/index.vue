<template>
  <section class="container"> 
    <div>
      <b-card-group deck>
        <nuxt-link
        v-for="post in posts"
        :key="post.id"
        :to="post.id"
        >
          <b-card
            footer="Card Footer"
            footer-tag="footer"
            :title="post.title">
          <b-card-img v-bind:src="post.thumbnailUrl"
                    alt="Image"
                    bottom></b-card-img>
          <p class="card-text">{{post.previewText}}.</p>
          </b-card> 
        </nuxt-link>
      </b-card-group>
    </div> 
  </section>
</template>

<script>

export default {
 data() {
   return {
     posts: [
       {
        title: 'A New Beginning',
        previewText: 'This will be awesome, don\'t miss it!',
        thumbnailUrl: 'https://picsum.photos/600/300/?image=24',
        id: 'a-new-beginning'
      },
      {
        title: 'A Second Beginning',
        previewText: 'This will be awesome, don\'t miss it!',
        thumbnailUrl: 'https://picsum.photos/600/300/?image=25',
        id: 'a-second-beginning'
      }
     ]
   }
 }
}
</script>

<style>

</style>
