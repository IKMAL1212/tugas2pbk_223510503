<template>
  <div id="app" class="full-screen" :style="{ backgroundColor: backgroundColor }">
    <div class="background">
      <div class="container" :style="{ color: textColor }">
        <h1>INPUT BIODATA</h1>
        <form @submit.prevent="submitForm">
          <div class="form-group">
            <label for="name">Nama:</label>
            <input type="text" id="name" :class="{ 'error': !formData.name }" v-model="formData.name" required>
            <span class="error-message" v-if="!formData.name">Masukan Nama Anda!</span>
          </div>
          <div class="form-group">
            <label for="email">Email:</label>
            <input type="email" id="email" v-model="formData.email" required>
          </div>
          <div class="form-group">
            <label for="message">Pesan:</label>
            <textarea id="message" v-model="formData.message" @input="updateDisplay" required></textarea>
          </div>
          <div class="form-group color-picker">
            <label for="backgroundColor">Background Color:</label>
            <input type="color" id="backgroundColor" v-model="backgroundColor">
          </div>
          <div class="form-group color-picker">
            <label for="textColor">Text Color:</label>
            <input type="color" id="textColor" v-model="textColor">
          </div>
          <button type="submit">Submit</button>
        </form>
      </div>
    </div>
    
    <div class="modal" v-if="showModal" @click="closeModal">
      <div class="modal-content" @click.stop>
        <span class="close" @click="closeModal">&times;</span>
        <h2>BIODATA ANDA</h2>
        <table>
          <tr>
            <td><strong>Name:</strong></td>
            <td>{{ formData.name }}</td>
          </tr>
          <tr>
            <td><strong>Email:</strong></td>
            <td>{{ formData.email }}</td>
          </tr>
          <tr>
            <td><strong>Message:</strong></td>
            <td>{{ formData.message }}</td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        name: '',
        email: '',
        message: ''
      },
      showModal: false,
      backgroundColor: '#f9f9f9',
      textColor: '#333'
    }
  },
  methods: {
    submitForm() {
      this.showModal = true;
    },
    closeModal() {
      this.showModal = false;
      this.resetForm();
    },
    resetForm() {
      for (let key in this.formData) {
        this.formData[key] = '';
      }
    },
    updateDisplay() {
    }
  }
}
</script>

<style scoped>
.full-screen {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.background {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  max-width: 600px;
  width: 100%;
}

.form-group {
  margin-bottom: 20px;
}

label {
  font-weight: bold;
}

input[type="text"],
input[type="email"],
textarea {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.color-picker {
  display: flex;
  align-items: center;
}

button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.close {
  position: absolute;
  top: 10px;
  right: 10px;
  cursor: pointer;
}
</style>
