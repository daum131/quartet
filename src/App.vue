<style>
  @import 'assets/style.css';
</style>
<template>
  <div id="app">
    <div class="conatainer mt-5">


      <div class="col form-inline-row">
        <select class="budget" v-model="selected">
          <option value='' selected>-- part --</option>
          <option value="Vn1">Vn1</option>
          <option value="Vn2">Vn2</option>
          <option value="Vn1">Va</option>
          <option value="Vn2">Vc</option>
        </select>

        <b-form-input v-model="newTask" placeholder="이름" @keyup.enter="add"></b-form-input>


        <b-button class="ml-2" variant="primary" @click="add">Add</b-button>
      </div>
    </div>


    <div class="row mt-3">
      <div class="col-md-3">
        <div class="p-2 alert alert-secondary">
          <h4>멤버</h4>
          <draggable class="list-group-row" :list="arrBacklog" group="tasks">
            <div class="list-group-item" v-for="element in arrBacklog" :key="element.name">
              {{ element.part}}
              {{ element.name}}
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-primary">
          <h4 class="edit room-1" @click="edit">음악실</h4>

          <div class="edit-wrap" style="display:none">
            <input v-model="message" placeholder="연습실 이름" class="roomNameInput">
            <button @click="change">변경</button>
          </div>

          <draggable class="list-group-row" :list="arrInporgress" group="tasks">
            <div class="list-group-item" v-for="element in arrInporgress" :key="element.name">
              {{ element.part}}
              {{element.name}}
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-warning">
          <h4 class="edit room-2" @click="edit_2">무용실</h4>

          <div class="edit-wrap_2" style="display:none">
            <input v-model="message" placeholder="연습실 이름" class="roomNameInput_2">
            <button @click="change_2">변경</button>
          </div>

          <draggable class="list-group-row" :list="arrTested" group="tasks">
            <div class="list-group-item" v-for="element in arrTested" :key="element.name">
              {{ element.part}}
              {{element.name}}
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-success">
          <h4>미술실</h4>
          <draggable class="list-group-row kanban-column" :list="arrDone" group="tasks">
            <div class="list-group-item" v-for="element in arrDone" :key="element.name">
              {{ element.part}}
              {{element.name}}
            </div>
          </draggable>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import draggable from "vuedraggable";


  export default {
    name: 'App',
    components: {
      draggable

    },
    data() {
      return {
        newTask: "",
        selected: "",
        arrBacklog: [{
            part: "Vn1",
            name: "송현진"
          },
          {
            part: "Va",
            name: "유관조"
          },
          {
            part: "Vn2",
            name: "이다음"
          },
          {
            part: "Vc",
            name: "황정원"
          }
        ],
        arrInporgress: [],
        arrTested: [],
        arrDone: [],
        message: "",
      };
    },
    methods: {
      add() {
        if (this.newTask) {
          this.arrBacklog.push({
            name: this.newTask,
            part: this.selected,
          });
          this.newTask = "";
        }
      },
      edit() {
        document.querySelector('.edit-wrap').style.display = "block"
      },
      change() {
        const rommName = document.querySelector('.roomNameInput').value;
        // document.querySelector(".roomNameInput").innerText = rommName;
        document.querySelector('.room-1').innerHTML = rommName;
        document.querySelector('.edit-wrap').style.display = "none"
      },
      edit_2() {
        document.querySelector('.edit-wrap_2').style.display = "block"
      },
      change_2() {
        const rommName = document.querySelector('.roomNameInput_2').value;
        // document.querySelector(".roomNameInput").innerText = rommName;
        document.querySelector('.room-2').innerHTML = rommName;
        document.querySelector('.edit-wrap_2').style.display = "none"
      }

    }
  }
</script>