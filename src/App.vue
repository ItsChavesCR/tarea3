<script>
export default {
  data() {
    return {
      contactos: [
        {
          nombre: "Gonzalo Gonzalez",
          trabajo: "Programador",
          celular: "8888-8888",
          email: "gonzalo@gmail.com",
          direccion: "San José"
        },
        {
          nombre: "Mario Maroto",
          trabajo: "Diseñador",
          celular: "7777-7777",
          email: "mario@gmail.com",
          direccion: "Heredia"
        }
      ],

      contactoSeleccionado: {
        nombre: "",
        trabajo: "",
        celular: "",
        email: "",
        direccion: ""
      },

      indiceSeleccionado: null
    }
  },

  methods: {

    seleccionarContacto(index) {

      this.indiceSeleccionado = index

      this.contactoSeleccionado = {
        ...this.contactos[index]
      }
    },

    agregarContacto() {

  const nuevoContacto = {
    nombre: "Nuevo Contacto",
    trabajo: "",
    celular: "",
    email: "",
    direccion: ""
  }

  this.contactos.push(nuevoContacto)

  this.indiceSeleccionado = this.contactos.length - 1

  this.contactoSeleccionado = {
    ...nuevoContacto
  }
},

    guardarContacto() {

      if (this.indiceSeleccionado !== null) {

        this.contactos[this.indiceSeleccionado] = {
          ...this.contactoSeleccionado
        }
      }
    },

    eliminarContacto() {

      if (this.indiceSeleccionado !== null) {

        this.contactos.splice(this.indiceSeleccionado, 1)

        this.indiceSeleccionado = null

        this.contactoSeleccionado = {
          nombre: "",
          trabajo: "",
          celular: "",
          email: "",
          direccion: ""
        }
      }
    }
  }
}
</script>

<template>

<div class="contenedor">

  <div class="lista">

    <h2>All Contacts</h2>

    <ul>

      <li
  :class="{ activo: indiceSeleccionado === index }"
        v-for="(contacto, index) in contactos"
        :key="index"
        @click="seleccionarContacto(index)"
      >
        {{ contacto.nombre }}
      </li>

    </ul>

    <button @click="agregarContacto">
      Add
    </button>

  </div>

  <div class="detalle">

    <label>Name:</label>
    <input v-model="contactoSeleccionado.nombre" />

    <label>Work:</label>
    <input v-model="contactoSeleccionado.trabajo" />

    <label>Mobile:</label>
    <input v-model="contactoSeleccionado.celular" />

    <label>Email:</label>
    <input v-model="contactoSeleccionado.email" />

    <label>Address:</label>
    <textarea v-model="contactoSeleccionado.direccion"></textarea>

    <div class="botones">

      <button @click="eliminarContacto">
        Delete
      </button>

      <button @click="guardarContacto">
        Save
      </button>

    </div>

  </div>

</div>

</template>

<style>

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  background: #f4f6f8;
  color: #1f2937;
}

.contenedor{
  display: flex;
  gap: 30px;
  padding: 40px;
  min-height: 100vh;
}


.lista{
  width: 320px;
  background: white;
  padding: 25px;
  border-radius: 16px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.05);
}

.lista h2{
  margin-bottom: 20px;
  font-size: 24px;
  color: #111827;
}

.lista ul{
  list-style: none;
}

.lista li{
  padding: 14px;
  margin-bottom: 12px;
  background: #f9fafb;
  border-radius: 10px;
  cursor: pointer;
  transition: 0.2s;
  border: 1px solid transparent;
}

.lista li:hover{
  background: #eef2ff;
  border-color: #6366f1;
  transform: translateY(-2px);
}

.lista li.activo{
  background: #6366f1;
  color: white;
  border-color: #6366f1;
}

.detalle{
  flex: 1;
  background: white;
  padding: 30px;
  border-radius: 16px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.05);

  display: flex;
  flex-direction: column;
}

.detalle label{
  margin-bottom: 8px;
  font-weight: 600;
  color: #374151;
}

.detalle input,
.detalle textarea{
  margin-bottom: 20px;
  padding: 14px;
  border: 1px solid #d1d5db;
  border-radius: 10px;
  outline: none;
  font-size: 15px;
  transition: 0.2s;
}

.detalle input:focus,
.detalle textarea:focus{
  border-color: #6366f1;
  box-shadow: 0 0 0 4px rgba(99,102,241,0.1);
}

.detalle textarea{
  min-height: 120px;
  resize: vertical;
}

.botones{
  display: flex;
  gap: 12px;
  margin-top: 10px;
}

button{
  padding: 12px 20px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  font-weight: 600;
  transition: 0.2s;
}

button:hover{
  transform: translateY(-1px);
}

.lista button{
  width: 100%;
  margin-top: 10px;
  background: #111827;
  color: white;
}

.lista button:hover{
  background: #1f2937;
}


.botones button:first-child{
  background: #ef4444;
  color: white;
}

.botones button:first-child:hover{
  background: #dc2626;
}

.botones button:last-child{
  background: #6366f1;
  color: white;
}

.botones button:last-child:hover{
  background: #4f46e5;
}

@media(max-width: 900px){

  .contenedor{
    flex-direction: column;
  }

  .lista{
    width: 100%;
  }

}

</style>