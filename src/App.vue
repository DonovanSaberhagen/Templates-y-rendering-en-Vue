<template>
  <div class="main-container">

    <!-- Inputs -->

    <form class="inputs-container">
      <div class="input-section">
        <label class="label-title" for="">Color de fondo</label>
        <input v-model="squarebackground" name="background" class="input" type="text" placeholder="Escriba un color" />
      </div>
      <div class="input-section">
        <label class="label-title" for="">Color de texto</label>
        <input v-model="squaretext" name="text" class="input" type="text" placeholder="Escriba un color" />
      </div>
      <div>
        <label class="custom-checkbox input-section">
          <label class="label-title" for="">Mostrar texto</label>
          <input v-model="showSpan" name="check" type="checkbox" />
          <span class="checkmark"></span>
        </label>
      </div>
      <div class="input-section">
        <label class="label-title" for="">Borde</label>
        <input v-model="borde" type="range" min="0" max="40" step="1" id="borde" />
      </div>
      <div class="input-section">
        <label class="label-title">Contenido textual</label>
        <textarea v-model="contenido" class="textarea" name="comentarios" rows="4" cols="25" maxlength="150"
          placeholder="Escribe aquí tus comentarios"></textarea>
      </div>
      <div class="input-section">
        <label class="label-title">Tipografía</label>
        <select v-model="textStyle" class="text-style" name="style-selection">
          <option v-for="(style, key) in textStyles" :key="key" :value="key">
            {{ style.label }}
          </option>
        </select>
      </div>
      <div class="input-section">
        <label class="label-title">Tamaño de letra</label>
        <div class="form-radio">
          <div>
            <input class="radio-selection" type="radio" name="radio-selected" id="pequeño" value="pequeño"
              v-model="fontSizesRadio" />
            <label for="pequeño">Pequeño</label>
          </div>
          <div>
            <input class="radio-selection" type="radio" name="radio-selected" id="mediano" value="normal"
              v-model="fontSizesRadio" />
            <label for="mediano">Mediano</label>
          </div>
          <div>
            <input class="radio-selection" type="radio" name="radio-selected" id="grande" value="grande"
              v-model="fontSizesRadio" />
            <label for="grande">Grande</label>
          </div>
        </div>
      </div>
    </form>
    <!-- cuadrado de estilo -->
    <div class="square-container">
      <div class="square" :style="{
        backgroundColor: squarebackground,
        color: squaretext,
        border: borde + 'px solid black',
      }">
        <span class="square-text" v-show="showSpan" :class="{
          [textStyles[textStyle].class]: true,
          'font-small': fontSizesRadio === 'pequeño',
          'font-normal': fontSizesRadio === 'normal',
          'font-large': fontSizesRadio === 'grande',
        }">
          {{ contenido }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      squarebackground: "", //color blanco de fondo
      squaretext: "", //texto
      showSpan: true, //on y off del span
      borde: "0", 
      contenido: "", 
      textStyle: "normal", 
      textStyles: {
        normal: { label: "Normal", class: "text-normal" },
        italic: { label: "Cursiva", class: "text-italic" },
        "line-through": { label: "Tachada", class: "text-line-through" },
        "line-through-italic": {
          label: "Tachada cursiva",
          class: "text-line-through-italic",
        },
        underline: { label: "Subrayada", class: "text-underline" },
        "underline-italic": {
          label: "Subrayada cursiva",
          class: "text-underline-italic",
        },
      },
      fontSizesRadio: "",
    };
  },
  name: "App",
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}

.main-container {
  display: flex;
  width: 100vw;
  height: auto;
}

.inputs-container {
  display: flex;
  flex-direction: column;
  margin: 3%;
  padding: 2%;
  width: 25%;
  background-color: #3b2f4f;
  border-radius: 30px;
}

.input-section {
  display: flex;
  flex-direction: column;
  row-gap: 10px;
  color: white;
  padding-bottom: 15px;

}

#borde {
  width: 200px;
}

.textarea {
  font-size: 16px;
  resize: none;
}

.text-style {
  height: 30px;
  width: 50%;
}

.label-title {
  font-size: 20px;
}

.form-radio {
  display: flex;
  gap: 10%;
}

.text-normal {
  font-style: normal;
}

.text-italic {
  font-style: italic;
}

.text-line-through {
  text-decoration: line-through;
}

.text-line-through-italic {
  font-style: italic;
  text-decoration: line-through;
}

.text-underline {
  text-decoration: underline;
}

.text-underline-italic {
  font-style: italic;
  text-decoration: underline;
}

.font-small {
  font-size: 12px;
  /* Pequeño */
}

.font-normal {
  font-size: 16px;
  /* Normal */
}

.font-large {
  font-size: 32px;
  /* Grande */
}



/*                       CSS                      */



.input {
  border: 2px solid transparent;
  width: 15em;
  height: 2.5em;
  padding-left: 0.8em;
  outline: none;
  overflow: hidden;
  background-color: #f3f3f3;
  border-radius: 10px;
  transition: all 0.5s;
}

.input:hover,
.input:focus {
  border: 2px solid white;
  box-shadow: 0px 0px 0px 7px rgba(43, 102, 158, 0.2);
  background-color: white;
}

/* div cuadrado  */

.square-container {
  padding-top: 12%;
  padding-left: 10%;
}

.square {
  margin-top: 10px;
  margin-left: 0%;
  height: 300px;
  width: 300px;
  border: 1px solid black;
  border-radius: 50px;
  background: #ffffff;
  box-shadow: 20px 20px 60px #d9d9d9, -20px -20px 60px #ffffff;
  align-items: center;
  display: flex;
  justify-content: center;
  word-wrap: break-word;
}

.square-text {
  width: 70%;
}

/* checkbox */

.custom-checkbox input[type="checkbox"] {
  display: none;
}

.custom-checkbox .checkmark {
  width: 24px;
  height: 24px;
  border: 2px solid white;
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 10px;
  transition: background-color 0.3s, border-color 0.3s, transform 0.3s;
  transform-style: preserve-3d;
}

.custom-checkbox .checkmark::before {
  content: "\2713";
  font-size: 16px;
  color: transparent;
  transition: color 0.3s, transform 0.3s;
}

.custom-checkbox input[type="checkbox"]:checked+.checkmark {
  background-color: #333;
  border-color: #333;
  transform: scale(1.1) rotateZ(360deg) rotateY(360deg);
}

.custom-checkbox input[type="checkbox"]:checked+.checkmark::before {
  color: #fff;
}

.custom-checkbox:hover .checkmark {
  border-color: #666;
  background-color: #f0f0f0;
  transform: scale(1.05);
}

.custom-checkbox input[type="checkbox"]:focus+.checkmark {
  box-shadow: 0 0 3px 2px rgba(0, 0, 0, 0.2);
  outline: none;
}

.custom-checkbox .checkmark,
.custom-checkbox input[type="checkbox"]:checked+.checkmark {
  transition: background-color 1.3s, border-color 1.3s, color 1.3s,
    transform 0.3s;
}
</style>
