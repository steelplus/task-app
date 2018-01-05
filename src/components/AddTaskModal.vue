<template>
  <div>
    <button class="btn tooltip tooltip-bottom centered" data-add-task-button data-tooltip="未アサインのタスクが表示されます。">
      UNASSIGNED TASKS <i class="icon icon-plus add-icon"></i>
    </button>
    <div class="modal modal-sm" data-add-task-modal id="modal-id">
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
          <button class="btn">
            <i class="icon icon-arrow-right"></i>
          </button>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
  /* eslint-disable object-shorthand,no-restricted-syntax */

  export default {
    name: 'add-task-modal',
    mounted: function mounted() {
      // モーダルを閉じる処理のバインド
      const taskModalElement = document.querySelector('[data-add-task-modal]');
      const closeButtons = taskModalElement.getElementsByTagName('a');
      for (const closeButton of closeButtons) {
        closeButton.addEventListener('click', () => {
          taskModalElement.classList.remove('active');
        });
      }

      // モーダルを開く処理のバインド
      const modalOpenButton = document.querySelector('[data-add-task-button]');
      modalOpenButton.addEventListener('click', () => {
        taskModalElement.classList.add('active');
      });
    },
  };
</script>

<style scoped>
  @import '../../node_modules/spectre.css/dist/spectre-icons.min.css';

  .content {
    position: relative;
  }

</style>
