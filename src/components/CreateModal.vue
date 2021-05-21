<template>
  <section id="create-modal" v-if="isModalOpen">
    <div class="overplay" @click="toggleAddModal"></div>
    <div class="modal-wrapper">
      <div class="modal-title"><h1>Thêm sinh viên</h1></div>
      <form class="modal-form">
        <input type="text" class="form-control" placeholder="Mã sinh viên" v-model="student.code" />

        <input
          type="text"
          class="form-control"
          placeholder="Họ và tên"
          v-model="student.fullName"
        />

        <label>
          <h3>Giới tính</h3>
          <div style="width: 60%">
            <input type="radio" name="gender" value="Nam" v-model="student.gender" />
            Nam
            <input type="radio" name="gender" value="Nữ" v-model="student.gender" />
            Nữ
            <input type="radio" name="gender" value="Khác" v-model="student.gender" />
            Khác
          </div>
        </label>

        <label for="hobby">
          <h3>Sở thích</h3>
          <textarea class="area" name="hobby" cols="30" rows="5" v-model="student.hobby"></textarea>
        </label>

        <button type="submit" class="btn btn--add mt-10" @click="addStudent">Lưu</button>
      </form>
    </div>
  </section>
</template>

<script>
  export default {
    name: 'CreateModal',
    data() {
      return {
        isModalOpen: false,
        student: {
          code: '',
          fullName: '',
          gender: 'Nam',
          hobby: '',
        },
      };
    },
    methods: {
      toggleAddModal() {
        this.isModalOpen = !this.isModalOpen;
      },

      addStudent() {
        let listStudents = JSON.parse(localStorage.getItem('listStudents'));
        listStudents.push(this.student);
        localStorage.setItem('listStudents', JSON.stringify(listStudents));
        this.$emit('addSuccess');
        this.toggleAddModal();
      },
    },
  };
</script>

<style scope>
  .mt-10 {
    margin-top: 10px;
  }

  textarea {
    resize: none;
  }

  input::placeholder {
    padding: 0 5px;
  }

  label {
    border: 1px solid #ccc;
    border-radius: 5px;
    margin-top: 10px;
    display: flex;
    justify-content: space-around;
    align-items: center;
    padding: 5px 0;
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.4);
  }

  #create-modal {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
  }
  .modal-title {
    padding: 0 25px;
  }
  #create-modal .overplay {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.3);
  }

  #create-modal .modal-wrapper {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 400px;
    height: 400px;
    background-color: #fff;
    border-radius: 15px;
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.4), -5px -5px 10px rgba(0, 0, 0, 0.4);
  }

  #create-modal .modal-wrapper h1 {
  }

  #create-modal .modal-wrapper h1::after {
    width: 120px;
  }

  #create-modal .modal-wrapper .modal-form {
    margin: 20px;
    display: flex;
    flex-direction: column;
  }

  #create-modal input[type*='text'].form-control {
    display: block;
    outline: none;
    border: none;
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.4);
    border-radius: 5px;
    height: 30px;
  }

  #create-modal .form-control + .form-control {
    margin-top: 10px;
  }
</style>
