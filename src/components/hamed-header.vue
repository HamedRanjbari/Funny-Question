<template>
  <div>
    <div>
      <b-navbar toggleable="lg" type="dark" variant="info" class="px-3">
        <b-navbar-brand href="#">Funny Question</b-navbar-brand>
        <b-navbar-brand href="#"
          >{{ correctCount }}/{{ totalCount }}</b-navbar-brand
        >
      </b-navbar>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    correctCount: Number,
    totalCount: Number,
  },
};
</script>
