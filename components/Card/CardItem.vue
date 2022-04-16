<template>
  <div
    :class="[
      'item-task d-flex align-items-start border-bottom pt-3 pb-4',
      isGrid ? 'col-12 col-md-6 col-lg-4' : 'col-12',
    ]"
  >
    <input
      type="checkbox"
      name="status"
      id="task"
      class="me-2 mt-2"
      :checked="!task.isDone"
      v-model="task.isDone"
    />
    <div v-if="!task.isDone" :class="['d-flex flex-column']">
      <div class="title-task mb-1">
        {{ task.title }}
        <span class="badge bg-info">{{ task.category }}</span>
      </div>
      <div class="description-task small text-muted">
        {{ task.description }}
      </div>
      <input type="date" class="form-control form-control-sm" />
    </div>
    <div v-else v-show="!task.isDone">
      <div class="title-task mb-1">
        {{ task.title }}
        <span class="badge bg-info">{{ task.category }}</span>
      </div>
      <div class="description-task small text-muted">
        {{ task.description }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    task: {
      type: Object,
      default: "Untitled",
    },
    isGrid: {
      type: Boolean,
      required: true,
      default: false,
    },
    
  },
};
</script>
