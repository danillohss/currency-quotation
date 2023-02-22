<template>
  <div class="container grid-lg my-2 py-2 text-dark">
    <div class="card">
      <div class="card-header">
        <div class="h4">Cotações das moedas</div>
      </div>
      <div class="card-body">
        <Table :quotes="quotes" />
      </div>
    </div>
  </div>
</template>

<script>
import Table from './components/Table'
import api from './services/api'
import { onMounted, reactive, toRefs } from 'vue';

export default {
  name: 'App',
  components: { Table },
  setup() {
    const data = reactive({
      quotes: {},
    });
    onMounted(async () => {
      const response = await api.all();
      data.quotes = response.data;
    })
    return { ...toRefs(data) }
  }
}
</script>

<style scoped>
.h4 {
  text-align: center;
  margin-bottom: 10px;
}

.card {
  box-shadow: inset 0 0 1em gold;
}
</style>
