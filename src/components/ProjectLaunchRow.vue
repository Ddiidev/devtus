<script setup>
import { computed } from 'vue'

const props = defineProps({
  project: {
    type: Object,
    required: true,
  },
})

const previewHref = computed(
  () => props.project.previewHref ?? props.project.actions?.[0]?.href ?? '#',
)
</script>

<template>
  <tr>
    <td class="project-table__preview-cell">
      <a
        class="project-preview"
        :href="previewHref"
        target="_blank"
        rel="noopener noreferrer"
        :aria-label="`Abrir ${project.title}`"
      >
        <img
          :src="project.image"
          :alt="`Preview de ${project.title}`"
          class="project-preview__image"
        />
      </a>
    </td>

    <td class="project-table__info-cell">
      <p class="project-title">{{ project.title }}</p>
      <p class="project-desc">{{ project.subtitle }}</p>
      <p class="project-url">{{ previewHref }}</p>
    </td>

    <td class="project-table__action-cell">
      <div class="project-actions">
        <a
          v-for="action in project.actions"
          :key="action.id"
          class="project-action"
          role="button"
          :href="action.href"
          target="_blank"
          rel="noopener noreferrer"
        >
          {{ action.label }}
        </a>
      </div>
    </td>
  </tr>
</template>
