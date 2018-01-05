<template>
  <draggable v-model="tasks" class="timeline-draggable" :options="dragOptions">
    <div v-for="task in tasks" :key="task.index">
      <task-card :task="task" />
    </div>
  </draggable>
</template>

<script>
  import Draggable from 'vuedraggable';
  import TaskCard from './TaskCard';

  export default {
    components: { TaskCard, Draggable },
    props: ['tasks'],
    name: 'time-line',
    computed: {
      dragOptions: function dragOptions() {
        return {
          animation: 0,
          group: 'task-card',
          ghostClass: 'ghost',
        };
      },
    },
  };
</script>

<style scoped>
  .timeline-draggable {
    min-height: 100%;
  }

  .ghost {
    opacity: .5;
    background: #C8EBFB;
  }
</style>
