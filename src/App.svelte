<script lang="ts">
  import { onMount, tick } from 'svelte'
  import tsartecShot from './assets/tsartec-shot.png'
  import geniaShot from './assets/genia-shot.jpeg'
  import realizaShot from './assets/realiza-shot.png'
  import joaoMemoji from './assets/joao-memoji.png'
  import bizziHeroSvg from './assets/bizzi-hero.svg?raw'

  type Locale = 'pt' | 'en'
  type Theme = 'dark' | 'light'

  type NavItem = {
    id: string
    pt: string
    en: string
  }

  type SkillGroup = {
    title: string
    items: string[]
  }

  type Project = {
    title: string
    description: string
    tags: string[]
    bullets?: string[]
    link?: string
    source?: string
    visual?: 'tsartec' | 'genia' | 'realiza' | 'study' | 'kirvo'
  }

  type ExperienceItem = {
    role: string
    company: string
    period: string
    description: string
  }

  type DetailItem = {
    title: string
    description: string
  }

  type LocaleContent = {
    metaTitle: string
    metaDescription: string
    available: string
    role: string
    heroTitle: string
    heroDescription: string
    viewProjects: string
    contactMe: string
    featuredEyebrow: string
    featuredTitle: string
    featuredDescription: string
    skillsEyebrow: string
    skillsTitle: string
    skillsDescription: string
    detailsEyebrow: string
    detailsTitle: string
    detailsDescription: string
    experienceEyebrow: string
    experienceTitle: string
    experienceDescription: string
    contactEyebrow: string
    contactTitle: string
    contactDescription: string
    talkButton: string
    contactPill: string
    themeLabel: string
    languageLabel: string
    nameLabel: string
    emailLabel: string
    messageLabel: string
    namePlaceholder: string
    emailPlaceholder: string
    messagePlaceholder: string
    sendLabel: string
    sendingLabel: string
    successLabel: string
    errorLabel: string
    footerCopy: string
    projectLink: string
    projectSource: string
    metrics: string[]
    projects: Project[]
    skillGroups: SkillGroup[]
    detailItems: DetailItem[]
    experienceItems: ExperienceItem[]
  }

  const navItems: NavItem[] = [
    { id: 'home', pt: 'Início', en: 'Home' },
    { id: 'projects', pt: 'Projetos', en: 'Projects' },
    { id: 'skills', pt: 'Habilidades', en: 'Skills' },
    { id: 'details', pt: 'Realiza', en: 'Realiza' },
    { id: 'experience', pt: 'Experiência', en: 'Experience' },
    { id: 'contact', pt: 'Contato', en: 'Contact' },
  ]

  const content: Record<Locale, LocaleContent> = {
    pt: {
      metaTitle: 'Joao Pedro | Portfolio',
      metaDescription:
        'Portfólio de João Pedro, desenvolvedor full stack júnior com experiência em Svelte, TypeScript, JavaScript, Go, PostgreSQL e automações.',
      available: 'Disponível para oportunidades full stack',
      role: 'Desenvolvedor full stack júnior',
      heroTitle: 'Olá, eu sou Joao Pedro',
      heroDescription:
        'Desenvolvedor full stack com foco em interfaces bem resolvidas, integrações, automações e produtos digitais que precisam funcionar de ponta a ponta.',
      viewProjects: 'Veja meus projetos',
      contactMe: 'Contate-me',
      featuredEyebrow: 'Resultados do mundo real',
      featuredTitle: 'Projetos e produtos em destaque',
      featuredDescription:
        'Aqui estão alguns trabalhos que representam bem meu momento atual: interfaces comerciais, sistemas reais, automações e produtos digitais que ajudam negócio e usuário ao mesmo tempo.',
      skillsEyebrow: 'Lista de tecnologias',
      skillsTitle: 'Habilidades',
      skillsDescription: 'Aqui estão algumas das tecnologias e frentes com as quais trabalho no dia a dia.',
      detailsEyebrow: 'Faculdade Realiza',
      detailsTitle: 'Experiência prática em sistemas, operação e produto no setor educacional.',
      detailsDescription:
        'Meu trabalho atual me colocou em contato direto com sistemas que precisam funcionar no dia a dia. Isso me deu base prática em manutenção, evolução de interface, integrações, automações e colaboração com o time.',
      experienceEyebrow: 'Experiência',
      experienceTitle: 'Uma trajetória em construção, já com base prática em ambiente profissional real.',
      experienceDescription:
        'Ainda estou no início da carreira, mas minha base já vem de contexto de produto, time, manutenção de sistemas, entregas reais e suporte a necessidades concretas do negócio.',
      contactEyebrow: 'Contato',
      contactTitle: 'Vamos construir algo bom.',
      contactDescription:
        'Atualmente estou disponível para trabalhar. Se você tem um projeto, produto ou operação que precisa de alguém com visão de front-end, back-end e automação, adoraria conversar. Email: jrodriguessilvaoliveira081@gmail.com',
      talkButton: 'Contato',
      contactPill: 'Contato',
      themeLabel: 'Tema',
      languageLabel: 'Idioma',
      nameLabel: 'Nome',
      emailLabel: 'Email',
      messageLabel: 'Mensagem',
      namePlaceholder: 'Seu nome',
      emailPlaceholder: 'seuemail@exemplo.com',
      messagePlaceholder: 'Escreva sua mensagem aqui...',
      sendLabel: 'Enviar',
      sendingLabel: 'Enviando...',
      successLabel: 'Mensagem enviada com sucesso. Vou te responder em breve.',
      errorLabel: 'Não foi possível enviar agora. Tente novamente em instantes.',
      footerCopy: '© 2026 Joao Pedro',
      projectLink: 'Ver projeto',
      projectSource: 'GitHub',
      metrics: [
        '1+ ano de experiência profissional',
        'Svelte como base forte no front-end',
        'Go e PostgreSQL como base complementar',
        'Produtos reais, integrações e automações',
      ],
      projects: [
        {
          title: 'Kirvo',
          description:
            'Plataforma SaaS de IA para times, construída do zero com um amigo. Conecta Slack, Linear, Gmail e GitHub numa interface de chat que entende o contexto do trabalho e age pelo time.',
          tags: ['React', 'TypeScript', 'Hono', 'IA', 'SaaS'],
          bullets: [
            'Design system próprio com tokens OKLCH e componentes acessíveis',
            'Backend em Hono com autenticação, banco de dados e API tipada end-to-end',
            'Turborepo com landing page, app autenticado e status page isolados',
          ],
          link: 'https://kirvo.app',
          visual: 'kirvo',
        },
        {
          title: 'tsartec',
          description:
            'A tsartec representa bem o tipo de trabalho que eu gosto de construir: presença digital com identidade forte, hierarquia visual clara e foco em conversão.',
          tags: ['Svelte', 'UI', 'Landing Page', 'Responsive'],
          bullets: [
            'Hero com mensagem mais direta e orientada à conversão',
            'Hierarquia visual pensada para leitura rápida',
            'Interface escura com acento de cor e linguagem mais moderna',
          ],
          link: 'https://tsartec.com/',
          source: 'https://github.com/pogbas21',
          visual: 'tsartec',
        },
        {
          title: 'GenIA',
          description:
            'Participação na construção de uma plataforma voltada a agentes de IA para marketing, combinando página comercial, fluxo autenticado e experiência de produto alinhada a operação real.',
          tags: ['Projeto real', 'IA', 'Marketing', 'Login'],
          link: 'https://www.genia.marketing/lp',
          visual: 'genia',
        },
        {
          title: 'Produtos internos na Faculdade Realiza',
          description:
            'Participação na manutenção e evolução de sistemas internos, CMS, LMS, CRM, banco de dados e ferramentas digitais voltadas ao setor educacional.',
          tags: ['Profissional', 'CMS', 'LMS', 'CRM'],
          visual: 'realiza',
        },
        {
          title: 'Base técnica em evolução contínua',
          description:
            'Estudos e implementações práticas com Svelte, TypeScript, JavaScript, Go, PostgreSQL, APIs, Git e automações para fortalecer minha entrega como desenvolvedor full stack.',
          tags: ['TypeScript', 'JavaScript', 'Go', 'APIs'],
          visual: 'study',
        },
      ],
      skillGroups: [
        {
          title: 'Frontend',
          items: ['Svelte', 'TypeScript', 'JavaScript', 'HTML', 'CSS', 'Responsividade', 'UI'],
        },
        {
          title: 'Backend e dados',
          items: ['Go', 'PostgreSQL', 'Integração com APIs', 'Banco de dados', 'REST API'],
        },
        {
          title: 'Produto e operação',
          items: ['CMS', 'LMS', 'CRM', 'Automações', 'Ferramentas internas', 'Boas práticas', 'Git', 'GitHub'],
        },
      ],
      detailItems: [
        {
          title: 'Sistemas internos em operacao',
          description:
            'Atuação em plataformas e ferramentas utilizadas no dia a dia da instituição, com foco em manutenção, evolução, estabilidade e continuidade operacional.',
        },
        {
          title: 'Contexto educacional e múltiplos produtos',
          description:
            'Contato com CMS, LMS, CRM e soluções de produtividade, o que fortaleceu minha leitura de produto e de necessidades reais de usuário.',
        },
        {
          title: 'Colaboracao com o time de tecnologia',
          description:
            'Trabalho próximo de um ambiente de entrega real, aprendendo com demandas concretas, ajustes contínuos, integrações e resolução de problemas técnicos.',
        },
      ],
      experienceItems: [
        {
          role: 'Desenvolvedor Full Stack Júnior',
          company: 'Faculdade Realiza',
          period: 'dez/2024 - atual',
          description:
            'Atuação no time de tecnologia com foco em desenvolvimento web, manutenção de sistemas internos, integrações, automações e evolução de soluções digitais para o setor educacional.',
        },
        {
          role: 'Formação complementar',
          company: 'Rocketseat - Discover',
          period: 'nov/2024',
          description:
            'Fundamentos da programação web com HTML, CSS, JavaScript, Git e GitHub.',
        },
      ],
    },
    en: {
      metaTitle: 'Joao Pedro | Portfolio',
      metaDescription:
        'Portfolio of Joao Pedro, a junior full stack developer working with Svelte, TypeScript, JavaScript, Go, PostgreSQL and automation workflows.',
      available: 'Available for full stack opportunities',
      role: 'Junior full stack developer',
      heroTitle: 'Hi, I am Joao Pedro',
      heroDescription:
        'Full stack developer focused on clear interfaces, reliable integrations, automation flows and digital products that need to work end to end.',
      viewProjects: 'See my work',
      contactMe: 'Contact me',
      featuredEyebrow: 'Real world results',
      featuredTitle: 'Featured projects and products',
      featuredDescription:
        'These are a few projects that represent where I am today: commercial interfaces, real systems, automation-oriented solutions and digital products designed to help both business and users.',
      skillsEyebrow: 'Technology list',
      skillsTitle: 'Skills',
      skillsDescription: 'Here are some of the technologies and areas I work with.',
      detailsEyebrow: 'Faculdade Realiza',
      detailsTitle: 'Hands-on experience with systems, operations and real educational products.',
      detailsDescription:
        'My current work put me in direct contact with systems that need to work every day. That gave me practical experience with maintenance, interface evolution, integrations, automation and team collaboration.',
      experienceEyebrow: 'Experience',
      experienceTitle: 'An early path, already shaped inside a real professional environment.',
      experienceDescription:
        'I am still early in my career, but my foundation already comes from real products, teamwork, business operations and practical problem solving.',
      contactEyebrow: 'Contact',
      contactTitle: 'Let us build something strong.',
      contactDescription:
        'I am currently available for work. If you have a project, product or operation that needs someone with frontend, backend and automation thinking, I would love to hear from you. Email: jrodriguessilvaoliveira081@gmail.com',
      talkButton: 'Contact',
      contactPill: 'Contact',
      themeLabel: 'Theme',
      languageLabel: 'Language',
      nameLabel: 'Name',
      emailLabel: 'Email',
      messageLabel: 'Message',
      namePlaceholder: 'Your name',
      emailPlaceholder: 'you@example.com',
      messagePlaceholder: 'Write your message here...',
      sendLabel: 'Send',
      sendingLabel: 'Sending...',
      successLabel: 'Message sent successfully. I will get back to you soon.',
      errorLabel: 'Could not send your message right now. Please try again shortly.',
      footerCopy: '© 2026 Joao Pedro',
      projectLink: 'View project',
      projectSource: 'GitHub',
      metrics: [
        '1+ year of professional experience',
        'Strong frontend foundation with Svelte',
        'Go and PostgreSQL as a complementary base',
        'Real products, integrations and automation',
      ],
      projects: [
        {
          title: 'Kirvo',
          description:
            'AI-powered SaaS platform for teams, built from scratch with a friend. Connects Slack, Linear, Gmail and GitHub into a chat interface that understands your team\'s work context and acts for you.',
          tags: ['React', 'TypeScript', 'Hono', 'AI', 'SaaS'],
          bullets: [
            'Custom design system with OKLCH tokens and accessible components',
            'Hono backend with authentication, database and typed end-to-end API',
            'Turborepo with isolated landing page, authenticated app and status page',
          ],
          link: 'https://kirvo.app',
          visual: 'kirvo',
        },
        {
          title: 'tsartec',
          description:
            'tsartec represents the kind of work I enjoy building: landing pages with strong identity, clear hierarchy and a focused browsing experience.',
          tags: ['Svelte', 'UI', 'Landing Page', 'Responsive'],
          bullets: [
            'Hero section with clearer conversion-focused messaging',
            'Visual hierarchy designed for fast reading',
            'Dark interface with a stronger color system',
          ],
          link: 'https://tsartec.com/',
          source: 'https://github.com/pogbas21',
          visual: 'tsartec',
        },
        {
          title: 'GenIA',
          description:
            'Participation in building a platform focused on AI agents for marketing, combining a commercial landing page, authenticated flow and a product experience aligned with real operations.',
          tags: ['Real project', 'AI', 'Marketing', 'Login'],
          link: 'https://www.genia.marketing/lp',
          visual: 'genia',
        },
        {
          title: 'Internal products at Faculdade Realiza',
          description:
            'Participation in the maintenance and evolution of internal systems, CMS, LMS, CRM, databases and digital tools for the education sector.',
          tags: ['Professional', 'CMS', 'LMS', 'CRM'],
          visual: 'realiza',
        },
        {
          title: 'Technical foundation in constant evolution',
          description:
            'Hands-on studies and implementations with Svelte, TypeScript, JavaScript, Go, PostgreSQL, APIs, Git and automation workflows to strengthen my full stack delivery.',
          tags: ['TypeScript', 'JavaScript', 'Go', 'APIs'],
          visual: 'study',
        },
      ],
      skillGroups: [
        {
          title: 'Frontend',
          items: ['Svelte', 'TypeScript', 'JavaScript', 'HTML', 'CSS', 'Responsive UI', 'UI'],
        },
        {
          title: 'Backend and data',
          items: ['Go', 'PostgreSQL', 'API integration', 'Databases', 'REST API'],
        },
        {
          title: 'Product and operations',
          items: ['CMS', 'LMS', 'CRM', 'Automation', 'Internal tools', 'Best practices', 'Git', 'GitHub'],
        },
      ],
      detailItems: [
        {
          title: 'Internal systems in production',
          description:
            'Work on platforms and tools used daily by the institution, with a focus on maintenance, improvement, stability and operational continuity.',
        },
        {
          title: 'Educational context and multiple products',
          description:
            'Exposure to CMS, LMS, CRM and productivity solutions, strengthening my product thinking and understanding of real user needs.',
        },
        {
          title: 'Collaboration inside the technology team',
          description:
            'Work close to a real delivery environment, learning from concrete demands, iterative adjustments, integrations and technical problem solving.',
        },
      ],
      experienceItems: [
        {
          role: 'Junior Full Stack Developer',
          company: 'Faculdade Realiza',
          period: 'Dec 2024 - Present',
          description:
            'Working within the technology team with a focus on web development, internal systems maintenance, integrations, automation and the evolution of digital solutions for education.',
        },
        {
          role: 'Complementary education',
          company: 'Rocketseat - Discover',
          period: 'Nov 2024',
          description:
            'Web programming fundamentals with HTML, CSS, JavaScript, Git and GitHub.',
        },
      ],
    },
  }

  let locale: Locale = 'pt'
  let theme: Theme = 'dark'
  let activeSection = 'home'
  let isScrolled = false
  let isMobileNav = false
  let isLocaleMenuOpen = false
  let navElement: HTMLElement | null = null
  let localeMenuElement: HTMLDivElement | null = null
  let heroSvgHost: HTMLDivElement | null = null
  let indicatorStyle = ''
  const navLinks = new Map<string, HTMLAnchorElement>()

  let contactName = ''
  let contactEmail = ''
  let contactMessage = ''
  let contactSubmitting = false
  let contactSucceeded = false
  let contactError = ''

  const applyTheme = (nextTheme: Theme) => {
    theme = nextTheme
    document.documentElement.dataset.theme = nextTheme
    localStorage.setItem('portfolio-theme', nextTheme)
  }

  const toggleTheme = () => {
    applyTheme(theme === 'dark' ? 'light' : 'dark')
  }

  const toggleLocale = () => {
    locale = locale === 'pt' ? 'en' : 'pt'
  }

  const localeOptions: Array<{ key: Locale; label: string; flag: string }> = [
    { key: 'pt', label: 'Português', flag: '🇧🇷' },
    { key: 'en', label: 'English', flag: '🇺🇸' },
  ]

  const current = () => content[locale]
  const currentLocaleOption = () => localeOptions.find((option) => option.key === locale) ?? localeOptions[0]
  const projectAlt = (title: string) => `${title} preview`
  const flatSkills = () => Array.from(new Set(current().skillGroups.flatMap((group) => group.items)))
  const syncViewportState = () => {
    isMobileNav = window.innerWidth <= 859
  }

  const toggleLocaleMenu = () => {
    isLocaleMenuOpen = !isLocaleMenuOpen
  }

  const selectLocale = (nextLocale: Locale) => {
    locale = nextLocale
    isLocaleMenuOpen = false
  }

  const handleNavClick = (id: string) => {
    activeSection = id
    if (!isMobileNav) {
      void updateIndicator()
    }

    const section = document.getElementById(id)
    if (!section) return

    const topbarHeight = document.querySelector<HTMLElement>('.topbar')?.offsetHeight ?? 0
    const extraOffset = window.innerWidth <= 560 ? 18 : 24
    const top = section.getBoundingClientRect().top + window.scrollY - topbarHeight - extraOffset

    window.scrollTo({
      top: Math.max(0, top),
      behavior: 'smooth',
    })
  }

  const navItemRef = (node: HTMLAnchorElement, id: string) => {
    navLinks.set(id, node)
    void updateIndicator()

    return {
      destroy() {
        navLinks.delete(id)
      },
    }
  }

  const updateIndicator = async () => {
    if (isMobileNav) {
      indicatorStyle = ''
      return
    }

    await tick()
    const activeLink = navLinks.get(activeSection)
    if (!activeLink || !navElement) return

    indicatorStyle = `width:${activeLink.offsetWidth}px;transform:translateX(${activeLink.offsetLeft}px);`
  }

  const initHeroGradients = () => {
    if (!heroSvgHost) return

    const svg = heroSvgHost.querySelector('svg')
    if (!svg) return

    const gradients = svg.querySelectorAll<SVGLinearGradientElement>('linearGradient[id^="linearGradient-"]')
    const ns = 'http://www.w3.org/2000/svg'

    gradients.forEach((gradient) => {
      if (gradient.querySelector('animate')) return

      const duration = 4.6 + Math.random() * 2.8
      const phase = Math.random() * duration
      const y2 = 93 + Math.random() * 8

      const configs = [
        { name: 'x1', from: '0%', to: '100%' },
        { name: 'x2', from: '0%', to: '95%' },
        { name: 'y1', from: '0%', to: '100%' },
        { name: 'y2', from: '0%', to: `${y2}%` },
      ]

      configs.forEach((config) => {
        const animate = document.createElementNS(ns, 'animate')
        animate.setAttribute('attributeName', config.name)
        animate.setAttribute('from', config.from)
        animate.setAttribute('to', config.to)
        animate.setAttribute('dur', `${duration}s`)
        animate.setAttribute('begin', `${-phase}s`)
        animate.setAttribute('repeatCount', 'indefinite')
        animate.setAttribute('calcMode', 'spline')
        animate.setAttribute('keySplines', '0.42 0 0.58 1')
        animate.setAttribute('keyTimes', '0;1')
        gradient.appendChild(animate)
      })
    })

    svg.querySelectorAll<SVGPathElement>('path[stroke^="url(#linearGradient-"]').forEach((path) => {
      path.style.strokeOpacity = '0.58'
    })

    const radialBase = svg.querySelector<SVGPathElement>('path[stroke="url(#paint0_radial_242_278)"]')
    if (radialBase) {
      radialBase.style.strokeOpacity = '0.035'
    }
  }

  const handleContactSubmit = async (event: SubmitEvent) => {
    event.preventDefault()
    contactSubmitting = true
    contactSucceeded = false
    contactError = ''

    try {
      const response = await fetch('https://formspree.io/f/mqegjnzl', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          Accept: 'application/json',
        },
        body: JSON.stringify({
          name: contactName,
          email: contactEmail,
          message: contactMessage,
        }),
      })

      if (!response.ok) {
        const data = await response.json().catch(() => null)
        throw new Error(data?.errors?.[0]?.message || current().errorLabel)
      }

      contactSucceeded = true
      contactName = ''
      contactEmail = ''
      contactMessage = ''
    } catch (error) {
      contactError = error instanceof Error ? error.message : current().errorLabel
    } finally {
      contactSubmitting = false
    }
  }

  onMount(() => {
    syncViewportState()
    const storedTheme = localStorage.getItem('portfolio-theme')
    applyTheme(storedTheme === 'light' ? 'light' : 'dark')

    const sections = navItems
      .map((item) => document.getElementById(item.id))
      .filter((section): section is HTMLElement => Boolean(section))

    const revealObserver = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (!entry.isIntersecting) return
          entry.target.classList.add('is-visible')
          revealObserver.unobserve(entry.target)
        })
      },
      {
        threshold: 0.16,
      },
    )

    document
      .querySelectorAll<HTMLElement>('.reveal, .reveal-stagger')
      .forEach((node) => revealObserver.observe(node))

    let ticking = false

    const onScroll = () => {
      isScrolled = window.scrollY > 18

      if (ticking) return
      ticking = true

      window.requestAnimationFrame(() => {
        const topbarHeight = document.querySelector<HTMLElement>('.topbar')?.offsetHeight ?? 0
        const probeLine = window.scrollY + topbarHeight + (window.innerWidth <= 859 ? 24 : 40)

        let nextActive = sections[0]?.id ?? 'home'

        sections.forEach((section) => {
          if (section.offsetTop <= probeLine) {
            nextActive = section.id
          }
        })

        if (nextActive !== activeSection) {
          activeSection = nextActive
          void updateIndicator()
        }

        ticking = false
      })
    }

    const onResize = () => {
      syncViewportState()
      isLocaleMenuOpen = false
      void updateIndicator()
      onScroll()
    }

    const onPointerDown = (event: PointerEvent) => {
      if (!isLocaleMenuOpen || !localeMenuElement) return
      if (localeMenuElement.contains(event.target as Node)) return
      isLocaleMenuOpen = false
    }

    const onKeyDown = (event: KeyboardEvent) => {
      if (event.key === 'Escape') {
        isLocaleMenuOpen = false
      }
    }

    onScroll()
    window.addEventListener('scroll', onScroll, { passive: true })
    window.addEventListener('resize', onResize)
    window.addEventListener('pointerdown', onPointerDown)
    window.addEventListener('keydown', onKeyDown)
    void updateIndicator()
    initHeroGradients()

    return () => {
      revealObserver.disconnect()
      window.removeEventListener('scroll', onScroll)
      window.removeEventListener('resize', onResize)
      window.removeEventListener('pointerdown', onPointerDown)
      window.removeEventListener('keydown', onKeyDown)
    }
  })
</script>

<svelte:head>
  <title>{current().metaTitle}</title>
  <meta name="description" content={current().metaDescription} />
</svelte:head>

<div class="page">
  <header class:scrolled={isScrolled} class="topbar">
    {#if !isMobileNav}
      <a class="brand" href="#home" aria-label="Voltar ao início">
        <span class="brand-mark">JP</span>
      </a>
    {/if}

    <nav class="nav" aria-label="Navegação principal" bind:this={navElement}>
      {#if !isMobileNav}
        <span class="nav-indicator" style={indicatorStyle}></span>
      {/if}
      {#each navItems as item}
        <a
          href={`#${item.id}`}
          class:active={activeSection === item.id}
          use:navItemRef={item.id}
          on:click|preventDefault={() => handleNavClick(item.id)}
        >
          {locale === 'pt' ? item.pt : item.en}
        </a>
      {/each}
    </nav>

    <div class="toolbar">
      <div class="locale-picker" bind:this={localeMenuElement}>
        <button
          class="toolbar-button locale-trigger"
          type="button"
          aria-label={current().languageLabel}
          aria-haspopup="menu"
          aria-expanded={isLocaleMenuOpen}
          on:click={toggleLocaleMenu}
        >
          <span class="locale-trigger-inner">
            <span class="locale-flag" aria-hidden="true">{currentLocaleOption().flag}</span>
            <span class="locale-chevron" aria-hidden="true">⌄</span>
          </span>
        </button>

        {#if isLocaleMenuOpen}
          <div class="locale-menu" role="menu" aria-label={current().languageLabel}>
            {#each localeOptions as option}
              <button
                class:active={locale === option.key}
                class="locale-option"
                type="button"
                role="menuitemradio"
                aria-checked={locale === option.key}
                on:click={() => selectLocale(option.key)}
              >
                <span aria-hidden="true">{option.flag}</span>
                <span>{option.label}</span>
              </button>
            {/each}
          </div>
        {/if}
      </div>

      <button class="toolbar-button" type="button" on:click={toggleTheme} aria-label={current().themeLabel}>
        {theme === 'dark' ? '☀' : '☾'}
      </button>
    </div>
  </header>

  <main>
    <section class="hero section" id="home">
      <div class="scene hero-scene" aria-hidden="true">
        <div class="hero-svg-wrap" bind:this={heroSvgHost}>
          {@html bizziHeroSvg}
        </div>
      </div>
      <div class="hero-inner reveal">
        <div class="hero-top">
          <div class="hero-avatar" aria-hidden="true">
            <img src={joaoMemoji} alt="" loading="eager" decoding="async" />
          </div>
          <div class="hero-badge-card">{current().available}</div>
        </div>
        <p class="hero-kicker">{current().role}</p>
        <h1>{current().heroTitle}</h1>
        <p class="hero-description">{current().heroDescription}</p>

        <div class="hero-actions">
          <a class="button button-primary" href="#projects">{current().viewProjects} <span aria-hidden="true">↓</span></a>
          <a class="button button-secondary" href="mailto:jrodriguessilvaoliveira081@gmail.com">👋 {current().contactMe}</a>
        </div>
      </div>
    </section>

    <section class="section" id="projects">
      <div class="section-header reveal">
        <p class="section-eyebrow">{current().featuredEyebrow}</p>
        <h2>{current().featuredTitle}</h2>
        <p>{current().featuredDescription}</p>
      </div>

      <div class="project-stack">
        {#each current().projects as project, index}
          <article class="card project-showcase reveal">
            <div class="project-copy">
              <div class="tag-list">
                {#each project.tags as tag}
                  <span>{tag}</span>
                {/each}
              </div>

              <h3>{project.title}</h3>
              <p>{project.description}</p>

              {#if project.bullets?.length}
                <ul class="bullet-list">
                  {#each project.bullets as bullet}
                    <li>{bullet}</li>
                  {/each}
                </ul>
              {/if}

              {#if project.link || project.source}
                <div class="link-row">
                  {#if project.link}
                    <a href={project.link} target="_blank" rel="noreferrer">{current().projectLink}</a>
                  {/if}
                  {#if project.source}
                    <a href={project.source} target="_blank" rel="noreferrer">{current().projectSource}</a>
                  {/if}
                </div>
              {/if}
            </div>

            <div class={`project-visual ${project.visual ?? 'study'}`}>
              {#if project.visual === 'kirvo'}
                <div class="kirvo-panel">
                  <div class="kirvo-panel-header">
                    <div class="kirvo-dot"></div>
                    <span class="kirvo-name">Kirvo</span>
                    <span class="kirvo-badge">IA</span>
                  </div>
                  <div class="kirvo-chat">
                    <div class="kirvo-msg kirvo-msg-system">O que vamos fazer hoje?</div>
                    <div class="kirvo-msg kirvo-msg-user">Resumir as issues abertas no Linear</div>
                    <div class="kirvo-msg kirvo-msg-system">Encontrei 4 issues para você revisar&nbsp;→</div>
                    <div class="kirvo-integrations">
                      {#each ['Slack', 'Linear', 'Gmail', 'GitHub'] as tool}
                        <span class="kirvo-chip">{tool}</span>
                      {/each}
                    </div>
                  </div>
                </div>
              {:else if project.visual === 'tsartec'}
                <img src={tsartecShot} alt={projectAlt(project.title)} loading="lazy" decoding="async" />
              {:else if project.visual === 'genia'}
                <img src={geniaShot} alt={projectAlt(project.title)} loading="lazy" decoding="async" />
              {:else if project.visual === 'realiza'}
                <img src={realizaShot} alt={projectAlt(project.title)} loading="lazy" decoding="async" />
              {:else}
                <div class="study-panel">
                  <div class="study-dots">
                    <span></span>
                    <span></span>
                    <span></span>
                  </div>
                  <div class="study-code">
                    <span>const stack = ['Svelte', 'TypeScript', 'Go']</span>
                    <span>buildUI(stack)</span>
                    <span>ship('real products')</span>
                  </div>
                </div>
              {/if}
            </div>
          </article>
        {/each}
      </div>
    </section>

    <section class="section" id="skills">
      <div class="section-header reveal">
        <p class="section-eyebrow">{current().skillsEyebrow}</p>
        <h2>{current().skillsTitle}</h2>
        <p>{current().skillsDescription}</p>
      </div>

      <div class="skills-cloud reveal-stagger">
        {#each flatSkills() as item, index}
          <span class="skill-pill stagger-item" style={`--stagger-index:${index}`}>{item}</span>
        {/each}
      </div>
    </section>

    <section class="section" id="details">
      <div class="section-header reveal">
        <p class="section-eyebrow">{current().detailsEyebrow}</p>
        <h2>{current().detailsTitle}</h2>
        <p>{current().detailsDescription}</p>
      </div>

      <div class="details-grid reveal-stagger">
        {#each current().detailItems as item, index}
          <article class="card detail-card stagger-item" style={`--stagger-index:${index}`}>
            <h3>{item.title}</h3>
            <p>{item.description}</p>
          </article>
        {/each}
      </div>
    </section>

    <section class="section" id="experience">
      <div class="section-header reveal">
        <p class="section-eyebrow">{current().experienceEyebrow}</p>
        <h2>{current().experienceTitle}</h2>
        <p>{current().experienceDescription}</p>
      </div>

      <div class="experience-list reveal-stagger">
        {#each current().experienceItems as item, index}
          <article class="card experience-card stagger-item" style={`--stagger-index:${index}`}>
            <div class="experience-top">
              <div>
                <p class="experience-role">{item.role}</p>
                <h3>{item.company}</h3>
              </div>

              <span class="experience-period">{item.period}</span>
            </div>

            <p>{item.description}</p>
          </article>
        {/each}
      </div>
    </section>

    <section class="section" id="contact">
      <div class="section-header reveal">
        <p class="section-eyebrow">{current().contactEyebrow}</p>
        <h2>{current().contactTitle}</h2>
        <p>{current().contactDescription}</p>
      </div>

      <div class="contact-shell reveal">
        <form class="card contact-form" on:submit={handleContactSubmit}>
          <div class="contact-grid">
            <label class="field">
              <span>{current().nameLabel}</span>
              <input
                bind:value={contactName}
                type="text"
                name="name"
                placeholder={current().namePlaceholder}
                required
                disabled={contactSubmitting}
              />
            </label>

            <label class="field">
              <span>{current().emailLabel}</span>
              <input
                bind:value={contactEmail}
                type="email"
                name="email"
                placeholder={current().emailPlaceholder}
                required
                disabled={contactSubmitting}
              />
            </label>
          </div>

          <label class="field">
            <span>{current().messageLabel}</span>
            <textarea
              bind:value={contactMessage}
              rows="6"
              name="message"
              placeholder={current().messagePlaceholder}
              required
              disabled={contactSubmitting}
            ></textarea>
          </label>

          {#if contactSucceeded}
            <div class="form-status form-status-success" role="status" aria-live="polite">
              <strong>OK</strong>
              <span>{current().successLabel}</span>
            </div>
          {/if}

          {#if contactError}
            <div class="form-status form-status-error" role="alert" aria-live="assertive">
              <strong>Erro</strong>
              <span>{contactError}</span>
            </div>
          {/if}

          <div class="contact-actions-bar">
            <button class="submit-button" type="submit" disabled={contactSubmitting}>
              {contactSubmitting ? current().sendingLabel : current().sendLabel}
              <span aria-hidden="true">→</span>
            </button>
          </div>
        </form>
      </div>
    </section>
  </main>

  <footer class="footer">
    <p>{current().footerCopy}</p>
    <div class="footer-links">
      <a href="https://github.com/pogbas21" target="_blank" rel="noreferrer">GitHub</a>
      <a href="https://www.linkedin.com/in/jo%C3%A3o-pedro-oliveira-209438337/" target="_blank" rel="noreferrer">LinkedIn</a>
    </div>
  </footer>
</div>
