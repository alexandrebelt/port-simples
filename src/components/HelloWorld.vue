<template>
  <section id="intro">
    <h1 class="title-ab">AB</h1>
    <div class="intro-text">
      <h3>
        <span class="span-text">L</span>
        <span class="span-text">o</span>
        <span class="span-text">r</span>
        <span class="span-text">e</span>
        <span class="span-text">m </span>
        <span class="span-text">I</span>
        <span class="span-text">p</span>
        <span class="span-text">s</span>
        <span class="span-text">u</span>
        <span class="span-text">m</span>

      </h3>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore
        magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
        consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla
        pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est
        laborum.</p>
    </div>
  </section>

  <section class="container limit">
    <ul class="lista-projetos">
      <li v-for="proj in projs" :key="proj.id" class="projeto">
        <a :href="proj.url">
          <div class="projeto-container">
            <h4>
              {{ proj.empresa }}
            </h4>
            <p>{{ proj.funcao }}</p>
            <p><span>Layout: </span> {{ proj.parceria }}</p>
          </div>
        </a>
      </li>
    </ul>
  </section>

  <section id="contato" class="container limit">
    <h1>Vamos trabalhar juntos?</h1>
    <form v-if="!isSended" ref="form" id="contact-form" @submit.prevent="sendEmail">
      <div class="form-content">
        <input required class="form-field" type="text" name="from_name" placeholder="Seu nome" />
        <hr class="form-hr">
        <input required class="form-field" type="email" name="reply_to" placeholder="Seu melhor e-mail " />
        <hr class="form-hr">
        <textarea required class="form-field" name="message" placeholder="Sua mensagem"></textarea>
        <hr class="form-hr">
        <button type="submit">
          <div class="loading-icon" v-if="isLoading">
            Carregando
          </div>
          <div v-else>
            Enviar
          </div>
        </button>
      </div>
    </form>
    <div v-else class="agradece">
      <p><span>Obrigado!</span> Entrarei em contato
        assim que possível. :)</p>
    </div>
  </section>

  <section id="footer container limit">
    <div id="credits">
      <a href="http://portfolio.alexandrebeltramini.com.br/">
        <div class="credits-wrapper">
          <h6>
            Code by AB
          </h6>
          <h6>
            Code by AB
          </h6>
        </div>
      </a>
    </div>
  </section>
</template>

<script>
import axios from 'axios';
import { defineComponent, ref } from 'vue'
import emailjs from '@emailjs/browser';
import gsap from 'gsap';
import ScrollTrigger from 'gsap/dist/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger)
export default {
  data() {
    return {
      projs: []
    }
  },
  mounted() {

    setTimeout(() => {
      axios.get('projetos.json')
        .then((res) => {
          this.projs = res.data
          console.log(this.projs)
        })
    }, 1000)
    var credit = document.querySelector('#credits');
    gsap.set('.title-ab', { y: 0 })

    gsap.to('.title-ab', {
      y: -100,
      scrollTrigger: {
        trigger: 'html',
        scrub: true,
        start: 'top top',
        end: '+=100'
      }
    })
    gsap.to('.intro-text', {
      scrollTrigger: {
        pin: true,
        trigger: '.intro-text',
        start: 'center center',
        end: 'center top',
        
      }
    })

    gsap.set('.span-text, .intro-text p', {
      opacity: 0
    })
    gsap.to('.span-text', {
      opacity:1,
      stagger:{amount: 0.2, from: "random"},
      scrollTrigger: {
        trigger: '.intro-text',
        start: 'center center',
        end: 'center 20%',
        scrub: 1
      }
    })
    gsap.to('.intro-text p', {
      opacity:1,
      scrollTrigger: {
        trigger: '.intro-text p',
        start: 'center 10%',
        end: 'center top',
        scrub: 1,
        markers: true,
      }
    })
 

    setTimeout(() => {

      gsap.to('.projeto', {
        stagger: 0.2,
        y: -100,
        scrollTrigger: {
          trigger: 'html',
          scrub: true,
          start: 'top top',
          end: 'bottom bottom'
        }
      })
    }, 1200);



    credit.addEventListener('mouseover', () => {
      gsap.to('#credits h6', { y: -15, duration: 0.8, ease: "power4.out" })
    })
    credit.addEventListener('mouseleave', () => {
      gsap.to('#credits h6', { y: 0, duration: 0.8, ease: "power4.out" })
    })
  },
  setup() {
    let isLoading = ref(false)
    let isSended = ref(false)
    const form = ref(null);

    const sendEmail = (e) => {
      e.preventDefault();
      isLoading.value = true;
      const currentForm = form.value;
      if (currentForm === null) return;

      emailjs.sendForm('service_g9jobfd', 'template_8bn97wn', currentForm, 'MSPIUEWF69QcjnYel')

        .then((result) => {
          isLoading.value = false;
          isSended.value = true;
          console.log(isLoading)
          const formulario = document.querySelector('.form-content');
          const obri = document.querySelector('.agradece');

          console.log('SUCCESS!', result.text);
          formulario?.classList.add('sended');
          obri?.classList.add('display')
          setTimeout(() => {
            formulario?.classList.add('off-display')
            obri?.classList.add('show')
          }, 500)

        })

        .catch((error) => {
          isLoading.value = false;
          console.error('FAILED...', error.text);
        });
    };

    return {
      form,
      sendEmail,
      isLoading
    };
  }
}
</script>

<style lang="scss">
#intro {
  height: 150vh;
  display: flex;
  flex-direction: column;

  .title-ab {
    margin-top: 40px;
  }

  .intro-text {
    max-width: 420px;
    text-align: left;
    margin: auto auto;

    h3 {
      font-family: var(--cotford);
      font-weight: 200;
      font-size: 24px;
    }
  }
}

.lista-projetos {
  list-style: none;
  padding: 0;
  display: flex;
  columns: 2;
  flex-wrap: wrap;
  justify-content: space-between;

  row-gap: 30px;

  .projeto {
    flex-basis: calc(50% - 15px);
    aspect-ratio: 1;
    height: 50%;
    background-color: #2b2b2b;
    border-radius: 20px;

    a {
      color: inherit;
      text-decoration: none;
      height: 100%;
      width: 100%;
      display: flex;

      .projeto-container {
        padding: 20px;

        align-content: center;
      }
    }

  }

}

#contato {
  h1 {
    margin-bottom: 80px;
    font-size: 38px;
  }
}

.form-field {
  background: none;
  border: none;
  font-family: var(--cotford);
  font-size: 32px;
  text-align: center;
  font-weight: 100;
  resize: none;
  color: #fff
}

.form-field::placeholder {
  font-weight: 300;
  opacity: 0.5;
}

.form-field:focus-visible {
  outline: none;
}


button {
  background: var(--cinza);
  border: 1px solid var(--preto);
  border-radius: 50%;
  transition: 1s;
  cursor: pointer;
  display: flex;
  margin: 40px auto 20px;
  color: #fff;

  &:hover {
    background: var(--preto);

    img {
      filter: invert(100%);
    }
  }
}

.loading-icon img {
  width: 2vw;
  animation-name: spin;
  animation-duration: 500ms;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
  animation-direction: reverse;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(360deg);
  }
}


.form-hr {
  width: 30px;
  margin: 20px auto;

}

textarea {
  padding-bottom: 2vw;
}

#contact-form {
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;

  .form-field {
    width: 100%;
  }

  textarea {
    width: 100%;
  }

}

#credits {
  cursor: pointer;
  width: fit-content;
  margin: 20px auto;

  .credits-wrapper {
    height: 15px;
    overflow: hidden;

    h6 {
      display: flex;
      line-height: 1.4em;
      color: inherit;
      color: #fff;

    }

  }
}
</style>