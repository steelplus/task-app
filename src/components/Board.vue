<template>
  <div class="columns timeline">
    <div class="column timeline-status1">
      <add-task-modal :add_task="add_task" />
      <time-line :tasks="status1" />
    </div>
    <div class="column timeline-status2">
      <button class="btn tooltip tooltip-bottom centered" data-tooltip="現在アサインされているタスクが表示されます。">ASSIGNED TASKS</button>
      <time-line :tasks="status2" />
    </div>
    <div class="column timeline-status3">
      <button class="btn tooltip tooltip-bottom centered" data-tooltip="完了したタスクが表示されます。">FINISHED TASKS</button>
      <time-line :tasks="status3" />
    </div>
  </div>
</template>

<script>
  import TaskCard from './TaskCard';
  import AddTaskModal from './AddTaskModal';
  import TimeLine from './TimeLine';

  export default {
    components: {
      TimeLine,
      AddTaskModal,
      TaskCard,
    },
    name: 'board',
    methods: {
      add_task: function addTask(subject, description, estimateHours) {
        this.status1 = this.status1.concat({
          subject,
          description,
          estimateHours,
          status: 'status1',
          // TODO ID採番
          id: this.status1.length + this.status2.length + this.status3.length + 1,
        });
      },
    },
    data() {
      return {
        status1: [
          {
            id: 1,
            projectId: '1',
            subject: 'タスク1',
            description: 'タスク1の説明文です。',
            estimateHours: '1',
            status: 'status1',
            index: 1,
          },
          {
            id: 2,
            projectId: '1',
            subject: 'タスク2',
            description: 'タスク2の説明文です。',
            estimateHours: '1.5',
            status: 'status1',
            index: 2,
          },
        ],
        status2: [
          {
            id: 3,
            projectId: '1',
            subject: 'タスク3',
            description: 'タスク3の説明文です。',
            estimateHours: '1.5',
            status: 'status1',
            index: 3,
          },
        ],
        status3: [],
        draggingTask: null,
      };
    },
  };
</script>

<style scoped lang="scss">
  .timeline {
    .timeline-status1 {
      background: #9edeee;
      padding-top: 3px;
    }

    .timeline-status2 {
      background: #91eec4;
      padding-top: 3px;
    }

    .timeline-status3 {
      background: #ffcacc;
      padding-top: 3px;
    }
  }
</style>
