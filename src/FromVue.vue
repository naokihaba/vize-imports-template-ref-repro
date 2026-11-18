<script setup lang="ts">
import { useTemplateRef } from "vue"

const form = useTemplateRef("form")

function validate() {
  return form.value?.reportValidity()
}
</script>

<template>
  <form ref="form" @submit.prevent="validate" />
</template>
