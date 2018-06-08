<template>
    <nuxt-link
        :to="id"
        >
          <b-card
            footer="Card Footer"
            footer-tag="footer"
            :title="post.title">
          <b-card-img v-bind:src="thumbnailImage"
                    alt="Image"
                    bottom></b-card-img>
          <p class="card-text">{{excerpt}}.</p>
          </b-card> 
        </nuxt-link>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            required: true
        },
        excerpt: {
            type: String,
            required: true
        },
        thumbnailImage: {
            type: String,
            required: true
        },
        id: {
            type: String,
            required: true
        }
    }
}
</script>

<style scoped>
a {
    text-decoration: none;
    color:black;
}

</style>

