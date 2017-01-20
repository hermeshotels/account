<template lang="html">
  <div>
    <q-data-table
      :data="table"
      :config="config"
      :columns="columns"
    >
      <!-- Custom renderer for "message" column -->
      <template slot="col-message" scope="cell">
        <span class="light-paragraph">{{cell.data}}</span>
      </template>
      <!-- Custom renderer for "source" column -->
      <template slot="col-source" scope="cell">
        <span v-if="cell.data === 'Audit'" class="label text-white bg-primary">
          Audit
          <q-tooltip>Some data</q-tooltip>
        </span>
        <span v-else class="label text-white bg-negative">{{cell.data}}</span>
      </template>
      <!-- Custom renderer when user selected one or more rows -->
      <template slot="selection" scope="selection">
        <button class="primary clear" @click="changeMessage(selection)">
          <i>edit</i>
        </button>
        <button class="primary clear" @click="deleteRow(selection)">
          <i>delete</i>
        </button>
      </template>
    </q-data-table>
  </div>
</template>

<script>
export default {
  mounted () {
    this.$http.get('https://api.ermeshotels.com/api/v1/channels/active').then((response) => {
      this.table = response.body.data
    }, (error) => {
      console.log(error)
    })
  },
  data () {
    return {
      config: {
        rowHeight: '50px',
        title: 'Hotels',
        refresh: true,
        columnPicker: true,
        responsive: true,
        pagination: {
          rowsPerPage: 15,
          options: [50, 100, 150]
        }
      },
      columns: [
        {
          label: 'Nome',
          field: 'name',
          filter: true
        },
        {
          label: 'Percentuale',
          field: 'perc',
          filter: true
        }
      ],
      table: []
    }
  }
}
</script>

<style lang="css">
</style>
