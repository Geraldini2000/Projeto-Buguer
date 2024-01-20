<template>
  <nav>

  </nav>

  <div class="container">

    <div class="box-left_c">

      <div class="box-left">

          <h1>Sunrise - Sunset finder</h1>
          
          <br>

          <form id="myForm">

            <select style="height: 50px !important;" class="fieldForm" v-model="options" required>
              <option value="" disabled selected><p>Selecione uma opção</p></option>
              <option value="rise">Sunrise</option>
              <option value="set">Sunset</option>
            </select>

            <input class="fieldForm" type="text" v-model="lat" placeholder="Latitude" required>
            
            <input class="fieldForm" type="text" v-model="lng" placeholder="Longitude" required>

            <button type="button" id="submit" name="submit" @Click="enviar()">Enviar contato</button>
          
        </form>

      </div>

    </div><!--box-left-->

    <div class="box-right">

      <img  src="../../public/img/painel-paisagem.webp" alt="imagem principal">

    </div>

  </div>
  
</template>

<script>
import axios from "axios";

  export default {
    name: 'Home',
    components: {
    
    },
    data(){
      return {
        lat: null,
        lng: null,
        options:null
      }
    },
    methods:{
      async enviar(){
        console.log("Select",this.options)
        console.log("latitude",this.lat)
        console.log("longitude",this.lng)
        var params = {
          lat : this.lat,
          lng : this.lng,
          type : this.options,
        }
        
        await axios.get("https://localhos/get/", { params }).then((res) => {
                console.log(res.data)
        })
        .catch((error) => {
                console.log(error);
        });
    } 
  }
}
</script>
<style>
:root{
    --green: #2ecc71;
    --red: #e74c3c;
    --main-color: #0682d1;
    --text-color: #FFFFFF;
    --text-dark: #C2CBE5;
    --background: #121725;
    --dark-grey: #2C344B;
    --light-grey: #5A668A;
}
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    text-decoration: none;
    list-style: none;
}
html{
    font-size: 62.5%;
}
body{
    margin: 0 auto;
    background-color: var(--background);
    color: var(--text-color);
    font-family: 'chivo', sans-serif;
    font-size: 1.6rem;
    position: relative;
}

body::-webkit-scrollbar {
    display: none;
}

img{
    max-width: 100%;
    border-radius: 1-px;
    object-fit: cover;
}

nav{
    padding: 3rem 5rem;
}

.container{
    margin: 0 auto;
    max-width: 100%;
    width: 1440px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-left: 5rem;
    position: relative;
}

/***************************************************************/
.box-left_c{
    background-color: var(--background);
    width: 50%;
    padding: 20px;
    position: relative;
    z-index: 999;
}

.box-right{
    width: 40%;
    position: absolute;
    right: 0px;
}
.box-right img{
   max-height: 750px;
}

h1{
    margin-bottom: 30px;
    font-size: 3.5rem;
    font-weight: 200;
    text-transform: uppercase;
}

h1 > span{
    color: var(--main-color);
}

p{
    margin-bottom: 30px;
    color: var(--text-dark);
    font-size: 1.8rem;
    width: 50rem;
    line-height: 2.8rem;
}

.fieldForm{
    background-color: var(--dark-grey);
    font-family: inherit;
    font-size: 1.6rem;
    width: 50rem;
    margin-top: 12px;
    margin-bottom: 12px;
    border: none;
    border-radius: 50px;
    padding: 1.5rem 2rem;
    outline: none;
    color: #FFFFFF;
}
 

.fieldForm:focus{
    outline: 1.5px dashed var(--light-grey);
    outline-offset: .5rem;
}

::placeholder{
    font-family: inherit;
    color: var(--text-dark);
    opacity: .5;
}

button{
    background-color: var(--main-color);
    color: var(--background);
    font-weight: 600;
    font-size: 1.6rem;
    font-family: inherit;
    width: 18rem;
    margin-left: -190px;
    border: none;
    border-radius: 50px;
    padding: 1rem;
    cursor: pointer;
    transition: .3s;
}

button:hover{
    background-color: var(--light-grey);
    color: var(--text-color);
}

.box-left > form{
    display: block;
}
h1 {
    color: var(--main-color);
 }
.image{ 
    padding-left: 10px;
    padding-right: 10px;
    max-width: 600px;
}

@media (max-width: 1160px){

    nav{
        display: none;
    }

    .box-right img{
        display: none;
    }

    .container{
        padding-left: 0;
        display: grid;
        align-items: center;
        justify-content: center;
    }

    .logo{
        width: 180px;
        display: block;
        margin: 5rem auto;
    }

    .box-left_c{
        margin: 0 auto;
        background-color: var(--background);
        opacity: .92;
        width: 100%;
        min-height: 100vh;
        display: grid;
        align-items: center;
        justify-content: center;
        padding: 5rem;
        text-align: center;
        position: absolute;
        top: 0;
        left: 0;
        z-index: 999;
    }
    h1{
        font-size: 3rem;
    }
    h3{
        font-size: 2rem;
    }

    p{
        margin: 0 auto;
        max-width: 100%;
        width: 40rem;
        padding-bottom: 30px;
    }

    .box-icons{
        width: 100%;
        order: 2;
        justify-content: center;
    }

}

@media (max-width: 550px){
    #slider img{
        width: 300px;
        margin-top: 200px;
    }

    .fieldForm{
        max-width: 100%;
        width: 35rem;
        margin-bottom: 0;
    }
    
    button{
        max-width: 100%;
        width: 35rem;
        margin-top: 15px;
        margin-left: 0px;
        margin-bottom: 10px;
    }

    .box-left_c{
        padding: 5rem 2rem;
    }

    .box-icons{
        margin-top: 50px;
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: center;
    }
    
    .box-icons > img{
        width: 15rem;
        padding: 20px;
    }

}


</style>
