<script setup>
import { computed, ref } from 'vue'
import ProjectLaunchRow from './components/ProjectLaunchRow.vue'
import { projects } from './data/projects'

const baseUrl = import.meta.env.BASE_URL
const activeTab = ref('projects')

const tabs = [
  { id: 'projects', label: 'Projetos' },
  { id: 'about', label: 'Sobre' },
]

const projectCount = computed(() => projects.length)
</script>

<template>
  <main class="desktop">
    <section class="window tools-window is-bright active" aria-label="TOOLS">
      <div class="title-bar active">
        <div class="title-bar-text">
          <img class="title-bar-icon" :src="`${baseUrl}favicon.svg`" alt="" aria-hidden="true" />
          <span>TOOLS</span>
        </div>
        <div class="title-bar-controls">
          <button type="button" aria-label="Minimize"></button>
          <button type="button" aria-label="Maximize"></button>
          <button type="button" aria-label="Close"></button>
        </div>
      </div>

      <div class="window-body has-space">
        <div class="shell">
          <header class="hero">
            <div class="hero__copy">
              <p class="eyebrow">devtu root</p>
              <h1>TOOLS</h1>
              <p class="hero__lead">
                Uma janela de entrada no estilo Windows 7, feita com a semântica correta do 7.css.
              </p>
            </div>
          </header>

          <menu role="tablist" class="tabs">
            <button
              v-for="tab in tabs"
              :key="tab.id"
              role="tab"
              type="button"
              :aria-selected="activeTab === tab.id"
              @click="activeTab = tab.id"
            >
              {{ tab.label }}
            </button>
          </menu>

          <section v-show="activeTab === 'projects'" role="tabpanel" class="tabpanel">
            <fieldset class="panel">
              <legend>Atalhos</legend>
              <p class="panel__lead">
                Cada projeto define suas próprias ações. Assim fica simples adicionar, remover ou
                trocar links depois.
              </p>

              <table class="project-table has-shadow">
                <colgroup>
                  <col class="project-table__preview-col" />
                  <col />
                  <col class="project-table__action-col" />
                </colgroup>
                <thead>
                  <tr>
                    <th scope="col">Preview</th>
                    <th scope="col">Projeto</th>
                    <th scope="col">Ação</th>
                  </tr>
                </thead>
                <tbody>
                  <ProjectLaunchRow v-for="project in projects" :key="project.id" :project="project" />
                </tbody>
              </table>
            </fieldset>
          </section>

          <section v-show="activeTab === 'about'" role="tabpanel" class="tabpanel">
            <div class="about-grid">
              <fieldset class="panel">
                <legend>Resumo</legend>
                <p class="panel__lead">
                  Root pública do devtu com aparência de aplicativo Windows 7, usando apenas
                  semantic HTML + CSS do 7.css + Vue.
                </p>
                <ul class="about-list">
                  <li>Interface aberta em uma única janela</li>
                  <li>Links sempre em nova aba</li>
                  <li>Adsense carregado no head</li>
                  <li>Previews reais dos destinos</li>
                </ul>
              </fieldset>

              <fieldset class="panel">
                <legend>Status</legend>
                <div class="status-cards">
                  <div class="status-card">
                    <span class="status-card__label">Projetos</span>
                    <strong>{{ projectCount }}</strong>
                  </div>
                  <div class="status-card">
                    <span class="status-card__label">Estilo</span>
                    <strong>7.css</strong>
                  </div>
                  <div class="status-card">
                    <span class="status-card__label">Adsense</span>
                    <strong>Ativo</strong>
                  </div>
                </div>
              </fieldset>
            </div>
          </section>

          <footer class="status-bar">
            <p class="status-bar-field">{{ projectCount }} itens visíveis</p>
            <p class="status-bar-field">janela TOOLS ativa</p>
            <p class="status-bar-field">ações modulares por projeto</p>
          </footer>
        </div>
      </div>
    </section>
  </main>
</template>
