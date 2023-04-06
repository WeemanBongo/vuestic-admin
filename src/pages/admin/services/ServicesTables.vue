<template>
  <div class="buttons">
    <div class="row">
      <div class="flex xs12">
        <va-card class="larger-padding">
          <va-card-title>{{ t('buttons.types') }}</va-card-title>
          <va-card-content class="row">
            <div class="flex">
              <va-button class="mr-2 mb-2"> {{ t('buttons.default') }}</va-button>
              <va-button class="mr-2 mb-2" disabled> {{ t('buttons.disabled') }}</va-button>
              <va-button class="mr-2 mb-2" preset="outline" border-color="primary" color="primary">
                {{ t('buttons.outline') }}</va-button
              >
              <va-button class="mr-2 mb-2" preset="outline" border-color="primary" color="primary" disabled>
                {{ t('buttons.disabled') }}</va-button
              >
              <va-button class="mr-2 mb-2" preset="plain"> {{ t('buttons.flat') }}</va-button>
              <va-button class="mr-2 mb-2" preset="plain" disabled> {{ t('buttons.disabled') }}</va-button>
            </div>
          </va-card-content>
        </va-card>
      </div>
    </div>
  </div>

  <div class="markup-tables flex">
    <va-card>
      <va-card-title>{{ t('tables.stripedHoverable') }}</va-card-title>
      <va-card-content>
        <div class="table-wrapper">
          <table class="va-table va-table--striped va-table--hoverable">
            <thead>
              <tr>
                <th>Name</th>
                <th>Email</th>
                <th>Country</th>
                <th>Status</th>
              </tr>
            </thead>

            <tbody>
              <tr v-for="user in users" :key="user.id">
                <td>{{ user.name }}</td>
                <td>{{ user.email }}</td>
                <td>{{ user.country }}</td>
                <td>
                  <va-badge :text="user.status" :color="getStatusColor(user.status)" />
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </va-card-content>
    </va-card>
  </div>
</template>

<script setup lang="ts">
  import { ref } from 'vue'
  import { useI18n } from 'vue-i18n'
  import data from '../../../data/services/data.json'

  const { t } = useI18n()

  const users = ref(data.splice(0, data.length))

  function getStatusColor(status: string) {
    if (status === 'paid') {
      return 'success'
    }

    if (status === 'processing') {
      return 'info'
    }

    return 'danger'
  }
</script>

<style lang="scss">
  .markup-tables {
    .table-wrapper {
      overflow: auto;
    }

    .va-table {
      width: 100%;
    }
  }
</style>
