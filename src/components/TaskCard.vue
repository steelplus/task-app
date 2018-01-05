<template>
  <div class="card task-card" draggable="true" :id="'task-card-'+ task.id" @dragstart="drag_start(task)">
    <div class="card-header">
      <div class="card-subject">
        <div class="card-title h5" @dblclick="click_subject(task.id, task.subject)">{{task.subject}}</div>
        <div class="form-group">
          <input class="form-input d-hide" @blur="change_title(task, titleInput.value)" type="text"
                 placeholder="task title">
        </div>
      </div>
      <div class="card-subtitle text-gray">担当者：test</div>
    </div>
    <div class="card-description">
      <div class="card-body" @dblclick="click_description(task.id, task.description)">{{task.description}}</div>
      <div class="form-group">
        <textarea class="form-input d-hide" placeholder="task description" rows="3"
                  @blur="change_description(task, descriptionInput.value)"></textarea>
      </div>
    </div>
    <div class="card-footer">
      Estimate Hour : {{task.estimateHours}}
    </div>
  </div>
</template>

<script>
  /* eslint-disable object-shorthand,no-param-reassign */

  const bindInputEvent = (inputElement, textElement, value, isCtrl) => {
    inputElement.value = value;
    inputElement.addEventListener('blur', () => {
      inputElement.classList.add('d-hide');
      textElement.classList.remove('d-hide');
    });
    inputElement.addEventListener('keydown', (e) => {
      if (e.key === 'Enter' && (!isCtrl || (isCtrl && e.ctrlKey))) {
        const evt = document.createEvent('HTMLEvents');
        evt.initEvent('blur', true, true);
        inputElement.dispatchEvent(evt);
      }
    });

    textElement.classList.add('d-hide');
    inputElement.classList.remove('d-hide');
    inputElement.focus();
  };

  export default {
    props: ['task', 'change_title', 'change_description', 'drag_start'],
    name: 'task-card',
    data() {
      return {
        titleInput: null,
        descriptionInput: null,
      };
    },
    methods: {
      click_subject: function clickSubject(id, subject) {
        // 要素の取得
        const subjectElement = document.getElementById(`task-card-${id}`).getElementsByClassName(
          'card-subject')[0].getElementsByClassName('card-title')[0];
        const inputElement = document.getElementById(`task-card-${id}`).getElementsByClassName(
          'card-subject')[0].getElementsByClassName('form-group')[0].getElementsByTagName('input')[0];
        this.titleInput = inputElement;

        // 値を変更する処理
        bindInputEvent(inputElement, subjectElement, subject, false);
      },
      click_description: function clickDescription(id, description) {
        const descriptionElement = document.getElementById(`task-card-${id}`).getElementsByClassName(
          'card-description')[0].getElementsByClassName('card-body')[0];
        const inputElement = document.getElementById(`task-card-${id}`).getElementsByClassName(
          'card-description')[0].getElementsByClassName('form-group')[0].getElementsByTagName('textarea')[0];
        this.descriptionInput = inputElement;

        // 値を変更する処理
        bindInputEvent(inputElement, descriptionElement, description, true);
      },
    },
  };
</script>

<style scoped>
  .task-card {
    margin-top: 3px;
    margin-bottom: 3px;
  }
</style>
