<template>
  <section id="home">
    <div class="container">
      <h1>Quản lý sinh viên</h1>
      <button class="btn btn--add" @click="toggleAddModal">Thêm sinh viên</button>
      <table class="table">
        <thead>
          <tr>
            <th v-for="(title, index) in listTitles" :key="index">
              {{ title }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(student, index) in listStudents" :key="index">
            <td>{{ index + 1 }}</td>
            <td>
              {{ student.code }}
            </td>
            <td>
              {{ student.fullName }}
            </td>
            <td>
              {{ student.gender }}
            </td>
            <td>
              {{ student.hobby }}
            </td>
            <td>
              <button type="button" class="btn btn--danger" @click="handleDeleteStudent(student)">
                Xóa
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <CreateModal ref="CreateModal" @addSuccess="addSuccess" />
  </section>
</template>

<script>
  import CreateModal from '@/components/CreateModal';
  export default {
    name: 'Home',
    data() {
      return {
        listTitles: ['STT', 'Mã Sinh Viên', 'Họ Và Tên', 'Giới Tính', 'Sở Thích', 'Hành Động'],
        listStudents: [],
      };
    },
    components: {
      CreateModal,
    },
    created() {
      this.listStudents = JSON.parse(localStorage.getItem('listStudents'));
      if (!this.listStudents) {
        localStorage.setItem('listStudents', JSON.stringify([]));
      }
    },
    methods: {
      toggleAddModal() {
        this.$refs.CreateModal.toggleAddModal();
      },
      handleDeleteStudent(studentWillDelete) {
        this.listStudents = this.listStudents.filter((student) => student !== studentWillDelete);
        localStorage.setItem('listStudents', JSON.stringify(this.listStudents));
      },
      addSuccess() {
        this.listStudents = JSON.parse(localStorage.getItem('listStudents'));
      },
    },
  };
</script>

<style>
  table,
  td,
  th {
    border: 1px solid #ddd;
    text-align: left;
  }

  table {
    border-collapse: collapse;
    width: 100%;
  }

  th,
  td {
    padding: 15px;
  }

  .btn {
    min-width: 120px;
    border: none;
    outline: none;
    height: 40px;
    border-radius: 5px;
    cursor: pointer;
    transition: opacity 0.3s linear;
    will-change: opacity;
    box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.2);
  }

  .btn:hover {
    opacity: 0.8;
  }

  .btn--add {
    color: #fff;
    background: linear-gradient(45deg, rgb(0, 0, 255), rgb(255, 255, 0));
  }

  .btn--danger {
    color: #fff;
    background-color: rgba(255, 0, 0, 0.837);
  }

  #home {
    overflow: hidden;
  }

  #home h1 {
    font-style: italic;
  }

  #home h1::after {
    content: '';
    display: block;
    width: 170px;
    margin-top: 3px;
    height: 2px;
    background: linear-gradient(45deg, red, blue);
  }

  #home .container {
    padding: 50px 135px;
    min-width: 1200px;
  }

  #home .table {
    max-width: 100%;
    width: 80%;
    margin: 20px 0;
  }
</style>
