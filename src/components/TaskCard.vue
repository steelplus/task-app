<template>
  <transition name="task">
    <div class="card task-card" draggable="true" :id="'task-card-'+ task.id">
      <div class="card-header">
        <div class="card-subject">
          <div class="card-title h5" v-show="labelShowState.subject" v-on:click="labelShowState.subject = false">
            {{task.subject}}
          </div>
          <div class="form-group" v-show="!labelShowState.subject">
            <input class="form-input" type="text" placeholder="task title" v-model="task.subject"
                   v-on:blur="labelShowState.subject = true" v-on:keyup.enter="labelShowState.subject = true">
          </div>
        </div>
        <!--TODO 担当者表示-->
        <div class="card-subtitle text-gray">担当者：test</div>
      </div>
      <div class="card-description">
        <div class="card-body" v-show="labelShowState.description" v-on:click="labelShowState.description = false">
          {{task.description}}
        </div>
        <div class="form-group" v-show="!labelShowState.description">
        <textarea class="form-input" placeholder="task description" rows="3"
                  v-model="task.description" v-on:blur="labelShowState.description = true"
                  v-on:keyup.enter.ctrl="labelShowState.description = true"></textarea>
        </div>
      </div>
      <div class="card-footer">
        Estimate Hour : {{task.estimateHours}}
      </div>
    </div>
  </transition>
</template>

<script>
  /* eslint-disable object-shorthand,no-param-reassign */
  export default {
    props: ['task'],
    name: 'task-card',
    data() {
      return {
        titleInput: null,
        descriptionInput: null,
        labelShowState: {
          subject: true,
          description: true,
        },
      };
    },
  };
</script>

<style scoped lang="scss">
  .task-card {
    margin-top: 3px;
    margin-bottom: 3px;
    cursor: move;
    .card-title {
      cursor: text;
    }
    .card-body {
      cursor: text;
    }
  }

  .task-enter-active, .task-leave-active {
    transition: opacity .2s;
  }

  .task-enter {
    opacity: .5;
  }
</style>
