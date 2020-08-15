<template>
  <div id="app">
    <div class="main-box">
      <h1>WhatsApp Messenger</h1>
      <p>Enter your destination number and message.
        Click send message to generate Whatsapp link.
      </p>
      <hr>
      <div class="form-group">
        <label class="form-label">to: </label>
        <input class="form-input" type="text" placeholder="081234xxxxxx" v-model="destination">
      </div>
      <div class="form-group">
        <label class="form-label">message: </label>
        <textarea class="form-input" rows="7" placeholder="this is my message" v-model="message"></textarea>
      </div>
      <button class="submit-button" v-on:click="handleSubmit()">
        <img class="whatsapp-logo" alt="Whatsapp-logo" src="https://img.icons8.com/color/48/000000/whatsapp.png">
        Send Message
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      destination: '',
      message: '',
      href: ''
    }
  },
  methods: {
    handleSubmit: function (){
      if (this.destination) {
        let des = this.destination.split('');

        if (des[0]==='+' && des[1]==='6' && des[2]==='2') des[0]='+';
        else if (des[0]==='0') des[0]='+62';
        else des.unshift('+62');

        let destination = des.join('');
        this.$set(this, 'href', `https://wa.me/${destination}?text=${this.message}`);
        window.open(this.href);
        return this.clearForm();
      } else {
        confirm("The destination field is required")
      }
    },
    clearForm: function () {
      this.$set(this, 'destination', '');
      this.$set(this, 'message', `link: ${window.location.href}`);
      this.$set(this, 'href', '');
    }
  },
  mounted: function () {
    this.$set(this, 'message', `link: ${window.location.href}`);
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.main-box {
  margin: 15px;
  width: 350px;
  height:auto;
  background:#cacaca;
  padding: 2px 15px 15px;
  border-radius:5px;
}
.form-group {
  margin: 10px 0;
  text-align: left;
}
.form-input {
  width: 98%;
  margin: 5px 0;
  padding: 3px;
  border-radius: 5px;
}
.submit-button {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;

  display: inline-block;
  margin-bottom: 0;
  font-weight: bold;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  cursor: pointer;
  background-image: none;
  padding: 6px 12px;
  font-size: 14px;
  line-height: 1.42857143;
  border-radius: 4px;
}
.whatsapp-logo {
  height: 20px;
  width: auto;
  vertical-align: middle;
}
</style>
