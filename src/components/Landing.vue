<script setup lang="ts">
import { onMounted } from 'vue';
import logo from '@/assets/logo_svg.svg';
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel'
import image1 from '@/assets/1.png';
import image2 from '@/assets/2.png';
import image3 from '@/assets/3.png';
import image4 from '@/assets/4.png';
import image5 from '@/assets/5.png';
import image6 from '@/assets/6.png';

const images = [
  {
     url: image1,
     title: 'Intuitivo.',
     text: 'Acesse as simulações de forma organizada.',
  },
  {
    url: image2,
    title: 'Sempre com você.',
    text: 'Conte com o tutor digital para compreender cada etapa do processo.',
  },
  {
    url: image3,
    title: 'Mão na massa.',
    text: 'Além da teoria, você mesmo vai realizar um processo do começo ao fim.',
  },
  {
    url: image4,
    title: 'Oops.',
    text: 'Aqui é um lugar seguro, se você errar, tudo bem. Vamos aprender e tentar de novo.',
  },
  {
    url: image5,
    title: 'Revise suas atividades.',
    text: 'Você pode revisar se está tudo correto antes de prosseguir para a próxima etapa.',
  },
  {
    url: image6,
    title: 'Sucesso!',
    text: 'Tenha o resumo do que aprendeu na simulação e prossiga para o próximo nível.',
  },
];

const changeHeaderWhenScroll = (header:any, navHeight:any) => {
  if (window.scrollY >= navHeight) {
    // scroll é maior que a altura do header
    header.classList.add('scroll')
  } else {
    // menor que a altura do header
    header.classList.remove('scroll')
  }
};

const scrollToAnchor = (anchorId:string) => {
  const target = document.getElementById(anchorId);
  if (target) {
    target.scrollIntoView({ behavior: 'smooth' });
  }
}

onMounted(() => {
  /*  abre e fecha o menu quando clicar no icone: hamburguer e x */
  const nav:any = document.querySelector('#header nav')
  const toggle = document.querySelectorAll('nav .toggle')

  for (const element of toggle) {
    element.addEventListener('click', function () {
      nav.classList.toggle('show')
    })
  }

  /* quando clicar em um item do menu, esconder o menu */
  const links = document.querySelectorAll('nav ul li a')

  for (const link of links) {
    link.addEventListener('click', function () {
      nav.classList.remove('show')
    })
  }

  /* mudar o header da página quando der scroll */
  const header:any = document.querySelector('#header')
  const navHeight = header.offsetHeight

  /* ScrollReveal: Mostrar elementos quando der scroll na página */
  // const scrollReveal = ScrollReveal({
  //   origin: 'top',
  //   distance: '30px',
  //   duration: 700,
  //   reset: true
  // })

  // scrollReveal.reveal(
  //   `
  //   #home .image, #home .text,
  //   #about .image, #about .text,
  //   #news .text, #news img, #news .news-card,
  //   #services header, #services .card,
  //   #contact .text, #contact .links,
  //   footer .brand, footer .social,
  //   #testimonials header, #testimonials .testimonials
  // `,{ interval: 100 }
  // )

  /* Botão voltar para o topo */
  const backToTopButton:any = document.querySelector('.back-to-top')

  function backToTop() {
    if (window.scrollY >= 560) {
      backToTopButton.classList.add('show')
    } else {
      backToTopButton.classList.remove('show')
    }
  }

  /* Menu ativo conforme a seção visível na página */
  const sections = document.querySelectorAll('main section[id]') as NodeListOf<HTMLElement>
  function activateMenuAtCurrentSection() {
    const checkpoint = window.pageYOffset + (window.innerHeight / 8) * 4

    for (const section of sections) {
      const sectionTop = section.offsetTop
      const sectionHeight = section.offsetHeight
      const sectionId = section.getAttribute('id')

      const checkpointStart = checkpoint >= sectionTop
      const checkpointEnd = checkpoint <= sectionTop + sectionHeight

      if (checkpointStart && checkpointEnd) {
        const menuLink = document.querySelector('nav ul li a[href*=' + sectionId + ']')
        if (menuLink) {
          menuLink.classList.add('active')
        }
      } else {
        const menuLink = document.querySelector('nav ul li a[href*=' + sectionId + ']')
        if (menuLink) {
          menuLink.classList.remove('active')
        }
      }
    }
  }

  /* When Scroll */
  window.addEventListener('scroll', function () {
    changeHeaderWhenScroll(header, navHeight);
    backToTop()
    activateMenuAtCurrentSection()
  })
 
});
</script>

<template>
  <header id="header">
      <nav class="container flex-direction-row">
        <a class="logo" href="#">
          <img :src="logo" class="logo_svg" />
        </a>
        <!-- MENU -->
        <div class="menu">
          <ul class="grid">
            <li><a class="title" href="#home">Início</a></li>
            <li><a class="title" href="#missao">Missão</a></li>
            <li><a class="title" href="#produto">Produto</a></li>
            <li><a class="title" href="#contact">Contato</a></li>
          </ul>
        </div>
        <!--FIM DO MENU-->
        <div class="toggle icon-menu"></div>
        <div class="toggle icon-close"></div>
      </nav>
    </header>
    <!-- Main -->
    <main>
      <!--Home-->
      <section class="section no-padding" id="home">
        <div class="width-100 relative">
          <div class="video-background absoulte z-index-1 width100">
            <video autoplay muted playsinline id="background-video" class="width100">
              <source src="@/assets/video_promo.mp4" type="video/mp4">
              Seu navegador não suporta vídeos.
            </video>
          </div>
          <div class="cortina absolute width100 height100" style="top: 0;"></div>
          <div class="container grid absolute z-index-2 hero-card sombra">
            <!-- <div class="image">
              <img src="@/assets/images/pets.png" alt="Imagem 1" />
            </div> -->
            <div class="text">
              <h2 class="title mb-0">
                Transforme <span class="font-16">a jornada</span>
              </h2>
              <h2 class="title">
                <span class="font-16">do seu</span> time <span class="font-17">com nosso</span> <span class="font-38 bold">simulador!</span>
              </h2>
              <p>
                <span class="bold">Eleve</span> a retenção de funcionários e reduza a curva de aprendizado com o nosso Simulador de Processos Logísticos!
              </p>
              <p>
                Esse simulador foi projetado para abranger os aspectos técnicos essenciais, proporcionando uma experiência técnica e interativa.
                Seu time poderá aprender de maneira envolvente e eficaz, aplicando conceitos técnicos na prática.
              </p>
            </div>
          </div>
        </div>
      </section>
      <div class="divider-1"></div>

      <!-- Missão -->
      <section class="section" id="missao">
        <div class="row">
          <div class="col col-6 pl-64 pr-64">
            <h2 class="title">Você sabia?</h2>
            <p>
              Cerca de 30% das empresas enfrentam desafios com a retenção e engajamento de funcionários devido à dificuldade em aprender e executar novas atividades.
            </p>
            <br />
            <p>
              Erros operacionais no setor de logística podem custar até 10% da receita anual das empresas, devido a falhas como atrasos e erros de manuseio.
            </p>
            <br />
            <p>
              Essas falhas podem representar milhões de reais em perdas para grandes operações.
              Reduzir esses erros através de um treinamento prático e interativo como o proposto pelo Simpply tem potencial para oferecer um retorno financeiro significativo, além de reduzir custos operacionais.
            </p>
            <br />
            <p>
              E se houvesse uma solução que resolvesse esses problemas, mas também transformasse a maneira como sua equipe aprende e executa tarefas?
              Imagine um treinamento que não só melhora a retenção e o engajamento, mas também reduz significativamente os erros operacionais.
            </p>
            <br />
            <p>
              Com o Simpply, você pode transformar esses desafios em oportunidades e alcançar resultados que antes pareciam inatingíveis.
              Não deixe que a falta de inovação continue a custar caro à sua empresa.
              Descubra como uma abordagem prática e interativa pode fazer toda a diferença!
            </p>
          </div>
          <div class="col col-6 pl-64 pr-64">
            <img
              class="mt-n128"
              src="@/assets/flag_supply.png"
              alt="Cãozinho e gatinho juntos"
            />
          </div>
        </div>
      </section>
      <div class="divider-2"></div>

     <!-- Produto -->
     <section class="section no-padding" id="produto" style="height: 800px;">
      <div class="absoulte z-index-1 width100 height100">
        <carousel :items-to-show="1" class="height100">
          <slide v-for="(slide, index) in images" :key="index" class="height100">
            <div class="carousel__item">
              <div id="carousel_img">
                <img :src="slide.url" />
              </div>
              <div class="absolute z-index-2 simulador-card sombra"
                style="top: 64px; right: 64px;"
              >
                <div class="text">
                  <h2 class="title">
                    {{ slide.title }}
                  </h2>
                  <p>{{ slide.text }}</p>
                </div>
              </div>
            </div>
          </slide>

          <template #addons>
            <navigation />
            <pagination />
          </template>
        </carousel>
      </div>
     </section>
     <div class="divider-1"></div>

      <!--Contato-->
      <section class="section" id="contact">
        <div class="container grid">
          <div class="text">
            <h2 class="title">Entre em contato com a gente</h2>
            <p>
              Quer melhorar a eficiência dos seus treinamentos técnicos e otimizar o desempenho da sua equipe de logística e comércio exterior?
              Estamos prontos para ajudar!
              Preencha o formulário e nossa equipe especializada entrará em contato com você rapidamente para entender suas necessidades e mostrar como nosso simulador pode transformar o aprendizado em sua empresa.
            </p>
            <p>
              Nosso compromisso é fornecer soluções personalizadas, focadas em reduzir o tempo de aprendizado e aumentar a retenção de colaboradores.
              Ao nos enviar uma mensagem, você dará o primeiro passo para revolucionar o treinamento técnico na sua organização, com uma experiência interativa e prática.
            </p>
            <p class="bold">Não perca tempo, fale com a gente agora!</p>
          </div>    
          <div class="links">
            <iframe src="https://docs.google.com/forms/d/e/1FAIpQLSer-FzzSrd42ChkeSRjOEZRgq2DS4y71Ci9l_fsGMGSkWue6w/viewform?embedded=true" frameborder="0" marginheight="0" marginwidth="0"
              class="frame_forms"
            >Carregando…</iframe>
          </div>
        </div>
      </section>

      <div class="divider-2"></div>

    </main>

    <!-- Footer -->
    <footer class="section">
      <div class="container grid">
        <div class="brand">
          <a class="logo logo-alt" href="#home"><img :src="logo" class="logo_svg" /></a>
          <p>@2024 Simpply</p>
          <p>Todos os direitos reservados.</p>
        </div>
        <!-- <div class="social grid">
          <a href="#" target="_blank"><i class="icon-instagram"></i> </a>
          <a href="#" target="_blank"><i class="icon-facebook"></i> </a>
          <a href="#" target="_blank"><i class="icon-youtube"></i> </a>
        </div> -->
      </div>
    </footer>
    <!-- Botão de voltar para topo -->
    <a href="#home" class="back-to-top"><i class="icon-arrow-up"></i></a>
</template>
