<template>
  <div>
    <button class="btn tooltip tooltip-bottom centered" data-add-task-button data-tooltip="未アサインのタスクが表示されます。">
      UNASSIGNED TASKS <i class="icon icon-plus add-icon"></i>
    </button>
    <div class="modal modal-sm" v-bind:class="{active : isModalActive}" data-add-task-modal id="modal-id">
      <a href="#close" class="modal-overlay" aria-label="Close"></a>
      <div class="modal-container">
        <div class="modal-header">
          <a href="#close" class="btn btn-clear float-right" aria-label="Close"></a>
          <div class="modal-title h5">新しいタスクの作成</div>
        </div>
        <div class="modal-body">
          <div class="content">
            <div class="form-group">
              <label class="form-label" for="new-task-subject">Subject</label>
              <input class="form-input input-sm" type="text" id="new-task-subject" placeholder="Subject">

              <label class="form-label" for="new-task-assignee">Assignee</label>
              <select class="form-select" id="new-task-assignee" multiple size="2">
                <option>-</option>
                <option>TEST-A</option>
                <option>TEST-B</option>
                <option>TEST-C</option>
              </select>

              <label class="form-label" for="new-task-description">Description</label>
              <textarea class="form-input" id="new-task-description" placeholder="Subject"></textarea>

              <label class="form-label" for="new-task-hour">Estimate hour</label>
              <input class="form-input input-sm" type="number" id="new-task-hour" placeholder="Estimate hour">
            </div>
          </div>
        </div>
        <div class="modal-footer">
          <button class="btn" data-register-btn
                  @click="add_task(subjectInput.value, descriptionInput.value, estimateHourInput.value)">
            登録
          </button>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
  /* eslint-disable object-shorthand,no-restricted-syntax */

  export default {
    props: ['add_task'],
    name: 'add-task-modal',
    data() {
      return {
        subjectInput: null,
        descriptionInput: null,
        estimateHourInput: null,
        isModalActive: false,
      };
    },
    mounted: function mounted() {
      // モーダルを閉じる(登録)処理のバインド
      const taskModalElement = document.querySelector('[data-add-task-modal]');
      const closeButtons = taskModalElement.getElementsByTagName('a');
      for (const closeButton of closeButtons) {
        closeButton.addEventListener('click', () => {
          this.isModalActive = false;
        });
      }
      const registerButton = document.querySelector('[data-register-btn]');
      registerButton.addEventListener('click', () => {
        this.isModalActive = false;
      });
      taskModalElement.addEventListener('keydown', (e) => {
        if (e.key === 'Enter' && e.ctrlKey) {
          const evt = document.createEvent('HTMLEvents');
          evt.initEvent('click', true, true);
          registerButton.dispatchEvent(evt);
        }
      });

      // モーダルを開く処理のバインド
      const modalOpenButton = document.querySelector('[data-add-task-button]');
      modalOpenButton.addEventListener('click', () => {
        this.isModalActive = true;
      });

      // 各input要素をdataにバインド
      this.subjectInput = document.getElementById('new-task-subject');
      this.descriptionInput = document.getElementById('new-task-description');
      this.estimateHourInput = document.getElementById('new-task-hour');
    },
  };
</script>

<style scoped>
  .content {
    position: relative;
  }

</style>
