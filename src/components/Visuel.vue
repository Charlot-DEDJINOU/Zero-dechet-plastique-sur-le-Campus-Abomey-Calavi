<script>
import { ref } from 'vue'
import { downloadImage } from './untils'
import robotImage from '@/assets/robot.jpg'

export default {
  name: 'Visuel-Back',
  setup() {
    const url_image = ref(robotImage)
    const name_file = ref({
      name: 'Aucun fichier choisi'
    })

    const declancheClick = (e) => {
      e.preventDefault()
      const input_file = document.getElementById('file2')
      input_file.click()
    }

    const InputChange = (event) => {
      name_file.value = event.target.files[0]

      if (name_file.value) {
        const reader = new FileReader()
        reader.onload = (e) => {
          const selectedFile = e.target.result
          url_image.value = selectedFile
        }
        reader.readAsDataURL(name_file.value)
      } else {
        name_file.value = 'Aucun fichier choisi'
      }
    }

    return {
      InputChange,
      declancheClick,
      url_image,
      name_file,
      downloadImage
    }
  }
}
</script>

<template>
  <div class="container d-flex flex-column align-items-center">
    <p class="my-4 text-center px-4 fs-3 fw-medium">Zéro déchet plastique sur le Campus d'Abomey-Calavi</p>
    <div class="visuel" id="visuel">
      <img class="image" :src="url_image" />
    </div>
    <p class="text-center my-3">Merci de choisir une photo de profil</p>
    <div class="my-3 upload">
      <button class="button" id="image" @click="declancheClick">
        Cliquez pour changer la photo
      </button>
      <i>{{ name_file.name }}</i>
    </div>
    <button class="download mb-5" @click="downloadImage()">Telecharger</button>
    <input type="file" id="file2" @change="InputChange" accept="image/*" hidden />
  </div>
</template>

<style>
.container {
  min-height: 100vh;
  height: auto;
  color: black;
  background-color: whitesmoke;
}
h3 {
  width: 500px;
}
.visuel {
  width: 500px;
  height: 500px;
  background-image: url(../assets/back.jpg);
  background-size: contain;
  background-position: center;
  display: flex;
  justify-content: flex-end;
  align-items: start;
}
.visuel .image {
  margin: 125px 40px 0px 0px;
  width: 160px;
  height: 160px;
  border-radius: 50%;
  border: 5px solid #fdc722;
  object-fit: cover;
}
.upload {
  width: 500px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.upload i {
  width: 200px;
  overflow-x: hidden;
}
.upload .button,
.download {
  background-color: #0d6f36;
  color: white;
  padding: 10px;
  border: none;
  border-radius: 5px;
  width: 250px;
}
.download {
  width: 500px;
  font-weight: 600;
}
@media (max-width: 500px) {
  .visuel {
    zoom: 0.65;
  }
  .upload {
    width: 100%;
    flex-direction: column;
  }
  .download,
  .upload .button,
  i {
    width: 100%;
  }
  i {
    margin: 10px auto;
  }
}
</style>
