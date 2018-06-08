<template>
    <div class="alert alert-warning alert-dismissible fade show" role="alert">
  <button type="button" class="close" data-dismiss="alert" aria-label="Close">
    <span aria-hidden="true">&times;</span>
  </button> {{messages}}
</div>
</template>

<script>
export default {
    name: 'alert',
    props:['messages'],
    data() {
        return {

        }
    }
}
</script>
