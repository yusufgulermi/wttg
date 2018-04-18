<template>
  <div id="app">
    <section id="content" class="section">
      <div class="container">
        <div class="columns is-centered">
          <div class="column is-three-quarters">
            <div class="box">
              <Content/>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import Content from './components/Content.vue'

export default {
  name: 'App',
  components: {
    Content
  }
}
</script>

<style>
@import 'buefy/lib/buefy.css';

#app {
  background-color: #f5f5f5;
  top: 0px;
  left: 0px;
  width: 100%;
  min-height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
#content {
  padding: 1.5rem 1.5rem;
  margin: 0;
}
</style>
