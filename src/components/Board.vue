<template>
  <div class="columns timeline">
    <div class="column timeline-status1" @dragover.prevent @drop="drag_drop('status1')">
      <button class="btn tooltip tooltip-right centered" data-tooltip="未アサインのタスクが表示されます。">UN ASSIGNED TASKS</button>
      <div v-for="task in status1">
        <task-card :task="task" :change_title="change_title" :change_description="change_description"
                   :drag_start="drag_start" />
      </div>
    </div>
    <div class="column timeline-status2" @dragover.prevent @drop="drag_drop('status2')">
      <button class="btn tooltip tooltip-bottom centered" data-tooltip="現在アサインされているタスクが表示されます。">ASSIGNED TASKS</button>
      <div v-for="task in status2">
        <task-card :task="task" :change_title="change_title" :change_description="change_description"
                   :drag_start="drag_start" />
      </div>
    </div>
    <div class="column timeline-status3" @dragover.prevent @drop="drag_drop('status3')">
      <button class="btn tooltip tooltip-left centered" data-tooltip="完了したタスクが表示されます。">FINISHED TASKS</button>
      <div v-for="task in status3">
        <task-card :task="task" :change_title="change_title" :change_description="change_description"
                   :drag_start="drag_start" />
      </div>
    </div>
  </div>
</template>

<script>
  import TaskCard from './TaskCard';

  export default {
    components: { TaskCard },
    name: 'board',
    methods: {
      change_title: function changeTitle(task, value) {
        // eslint-disable-next-line no-param-reassign
        task.subject = value;
      },
      change_description: function changeDescription(task, value) {
        // eslint-disable-next-line no-param-reassign
        task.description = value;
      },
      drag_start: function dragStart(task) {
        this.draggingTask = task;
      },
      drag_drop: function dragDrop(status) {
        this[this.draggingTask.status] =
          this[this.draggingTask.status].filter(elm => elm.id !== this.draggingTask.id);
        this[status] = this[status].concat(this.draggingTask);
        this.draggingTask.status = status;
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
          },
          {
            id: 2,
            projectId: '1',
            subject: 'タスク2',
            description: 'タスク2の説明文です。',
            estimateHours: '1.5',
            status: 'status1',
          },
          {
            id: 3,
            projectId: '1',
            subject: 'タスク3',
            description: 'タスク3の説明文です。',
            estimateHours: '1.5',
            status: 'status1',
          },
        ],
        status2: [],
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
