<template>
  <main id="home">
    <section class="ctn_name">
      <section class="fixed">
        <div class="name">
          <h1>
            Martina Fernandez
            <br>Suarez Anzorena
          </h1>
          <div class="asterisk">
            <img src="/images/asterisk.svg" alt="">
          </div>
        </div>
        <div class="leftMargin whiteText">
            <div class="single-line">
              <div class="single-line-inner">
                <p class="generalText">Passionate about creating modern websites.</p>
              </div>
            </div>
            <div class="single-line">
              <div class="single-line-inner">
                <p class="generalText">Always looking forward to finding new</p>
              </div>
            </div>
            <div class="single-line">
              <div class="single-line-inner">
                <p class="generalText">challenging projects.</p>
              </div>
            </div>
        </div>
        <div id="webDev" class="first-scroll single-line">
          <div class="single-line-inner">
            <p>Web Developer</p>
          </div>
        </div>
      </section>
    </section>
    <section id="works" class="second-scroll">
      <div id="ctn_projects">
        <h2 class="title orangeText">Works</h2>
        <div class="cards">
          <div v-for="(project, i) in projects" :key="i">
            <ProjectCard :project="project" @projectSelected="handleModal"/>
          </div>
        </div>
      </div>
    </section>
    <Modal :project="projectSelected" v-if="viewModal" @closeModal="closeModal"/>
  </main>
</template>
<script setup lang="ts">
  import { onBeforeMount, onMounted, onUnmounted, ref } from 'vue';
  import gsap from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  import Modal from '@/components/Modal.vue';
  import ProjectCard from '@/components/ProjectCard.vue';
  import projectsJson from '../assets/data/projectsData.json';

  //PROJECTS
  const projects = ref<any[]>(projectsJson);
  const viewModal = ref(false);
  const projectSelected = ref()
  
  onBeforeMount(() => {
    projects.value = projectsJson;
  });

  function handleModal (project: any) {
    projectSelected.value = project;
    viewModal.value = true;
    return;
  }

  function closeModal() {
    viewModal.value = false;
    return;
  }

  //SCROLL ANIMATIONS
  onMounted(() => {
  gsap.registerPlugin(ScrollTrigger);

  // Timeline for scroll-triggered animations
  const tl = gsap.timeline();

  // First scroll animation: faster + smoother easing
  tl.fromTo('.first-scroll',
    {
      xPercent: 0,
    },
    {
      xPercent: 200,
      duration: 1.2, // reduced from 2.5 to make it faster
      ease: "power2.out", // smoother easing
      scrollTrigger: {
        trigger: '#home',
        start: '20% 30%',
        end: 'bottom 70%',
        scrub: true,
        markers: false,
        id: 'trigger-1',
      }
  });

  // Second scroll animation: smoother
  tl.fromTo('#works',
    {
      yPercent: 100,
    },
    {
      duration: 3,
      yPercent: 0,
      ease: 'power2.out',
      scrollTrigger: {
        trigger: '#home',
        start: 'top 0%',
        end: 'bottom 20%',
        scrub: true,
        markers: false,
        id: 'trigger-2',
      },
    }, '+=6'); // reduced delay to make the entrance more natural
});

  onUnmounted(() => {
    ScrollTrigger.getAll().forEach((trigger) => trigger.kill());
  });

</script>