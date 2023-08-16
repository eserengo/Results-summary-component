<template>
  <main class="main">
    <section class="sectionA">
      <h1 class="title normal">Your Result</h1>
      <div v-cloak class="divA">
        <span class="spanA bold">{{ setResult }} </span>
        <span class="spanB normal">of 100</span>
      </div>
      <h2 class="bold">Great</h2>
      <p class="para normal">You scored higher than 65% of the people who have taken this tests.</p>
    </section>
    <section class="sectionB">
      <h1 class="title bold">Summary</h1>
      <div v-for="(item, index) in fetchedData" :key="`key_${index}`" :class="`divB i_${index}`">
        <img :src="item.icon" :alt="`${item.category} icon`" />
        <span class="bold break category">{{ item.category }}</span>
        <span class="bold score">{{ item.score }}</span>
        <span class="rest">/&nbsp;100</span>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: "ResultsSummary",
  data() {
    return {
      fetchedData: [],
    }
  },
  methods: {
    async getData() {
      try {
        const res = await fetch('../src/assets/data.json');
        const json = await res.json();
        this.fetchedData = json;
      } catch (error) {
        this.fetchedData.push(error);
      }
    },
  },
  computed: {
    setResult() {
      return this.fetchedData
        && Math.trunc(this.fetchedData.map(item => item.score).reduce((a, b) => a + b) / 4);
    },
  },
  created() {
    this.getData();
  },
}
</script>