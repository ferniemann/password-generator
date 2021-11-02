<template>
<form class="options" id="options" onsubmit="return false" @input="generatePassword()">
  <div class="character-set">
    <div class="lowercase">
      <input type="checkbox" name="characters" id="pw-lowercase" checked>
      <label for="pw-lowercase" class="char-category">Lowercase</label>
    </div>
    <div class="uppercase">
      <input type="checkbox" name="characters" id="pw-uppercase">
      <label for="pw-uppercase" class="char-category">Uppercase</label>
    </div>
    <div class="numbers">
      <input type="checkbox" name="characters" id="pw-numbers">
      <label for="pw-numbers" class="char-category">Numbers</label>
    </div>
    <div class="special">
      <input type="checkbox" name="characters" id="pw-symbols">
      <label for="pw-symbols" class="char-category">Symbols</label>
    </div>
  </div>
  <div class="slider">
    <label for="pw-length">Password Length:</label><br>
    <input type="range" name="" id="pw-length" :value="value" min="8" max="35" step="1" @input="updateValue()">
    <label for="pw-length" class="slider-value">{{ value }}</label>
  </div>
</form>
  <div class="result">
    <p id="generated-password">{{ generatedPassword }}</p>
    <button @click="copyPassword()">
      <i class="fas fa-clipboard"></i>
      Copy to Clipboard
    </button>
    <p class="success" id="success">Password was succesfully copied to your clipboard!</p>
  </div>
</template>

<script>
export default {
  name: "PasswordGenerator",

  data() {
    return {
      value: 8,
      generatedPassword: "abcdefgh",
      lowercaseCharacters: "abcdefghijklmnopqrstuvwxyz",
      uppercaseCharacters: "ABCDEFGHIJKLMNOPQRSTUVWXYZ",
      numbers: "0123456789",
      symbols: "!§$%&/()=?¡¢[]|{}"
    }
  },

  methods: {
    updateValue() {
      this.value = document.getElementById("pw-length").value
      return this.value
    },

    generatePassword() {
      let length = this.value
      let charTypes = "a-z"
      let charArray = charTypes.split(",")
      let charSet = ""
      this.generatedPassword = ""
      const addUppercase = document.getElementById("pw-uppercase")
      const addNumbers = document.getElementById("pw-numbers")
      const addSymbols = document.getElementById("pw-symbols")

      if (charArray.indexOf("a-z") >= 0) {
        charSet += "abcdefghijklmnopqrstuvwxyz"
      }

      if (addUppercase.checked) {
        charTypes = charTypes.concat(",A-Z")
        console.log(charTypes)
      } else if (!addUppercase.checked) {
        charTypes = charTypes.replace(",A-Z", "")
        console.log(charTypes)
      }

      if (addNumbers.checked) {
        charTypes = charTypes.concat(",0-9")
      }

      for (let i = 0; i < length; i++) {
        this.generatedPassword += charSet.charAt(Math.floor(Math.random() * charSet.length))
      }

      return this.generatedPassword
    },

    copyPassword() {
      const successMessage = document.getElementById("success")
      let password = document.getElementById("generated-password").innerText
      navigator.clipboard.writeText(password)
      successMessage.style.visibility = "visible"
      setTimeout(function () {
        successMessage.style.visibility = "hidden"
      }, 3500)
    }
  },

  mounted() {
    this.generatePassword()
  }
}
</script>

<style scoped>
  .character-set {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 2rem;
    margin: 2rem 0;
  }

  .character-set input[type="checkbox"] {
    display: none;
  }

  .char-category {
    color: rgba(255 255 255 / .5);
    border: 2px solid rgba(255 255 255 / .5);
    padding: .25rem .5rem;
    border-radius: .2rem;
  }

  input[type="checkbox"]:checked + .char-category {
    background: var(--color-secondary);
    color: var(--color-light);
    border-color: var(--color-secondary);
  }

  .slider * {
    margin: .5rem 0;
  }

  .slider-value {
    display: inline-block;
    width: 2rem;
  }

  .result {
    margin: 2rem 0;
  }

  .result p:first-of-type {
    background: rgba(255 255 255 / .1);
    padding: .5rem 1rem;
    border-radius: .1rem;
    word-wrap: break-word;
    margin: 1rem 0;
  }

  button {
    background-color: var(--color-secondary);
    border: none;
    padding: .25rem .5rem;
    border-radius: .1rem;
  }

  .success {
    background-color: var(--color-success);
    display: inline-block;
    font-size: .75rem;
    color: var(--color-dark);
    width: 70vw;
    margin-top: 1rem;
    padding: .25rem;
    border-radius: .2rem;
    visibility: hidden;
    transition: visibility 1s;
  }
</style>