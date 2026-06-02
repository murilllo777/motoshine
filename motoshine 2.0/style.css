/* =============================================
   MOTOSHINE v2.0 — script.js
   Funcional, sem número falso, sem contador fake
   ============================================= */

(function () {
  'use strict';

  /* ---- HEADER: scroll effect ---- */
  const header = document.getElementById('header');
  if (header) {
    window.addEventListener('scroll', () => {
      header.classList.toggle('scrolled', window.scrollY > 40);
    }, { passive: true });
  }

  /* ---- HAMBURGER / MOBILE MENU ---- */
  const hamburger = document.getElementById('hamburger');
  const mobileMenu = document.getElementById('mobileMenu');

  if (hamburger && mobileMenu) {
    hamburger.addEventListener('click', () => {
      const isOpen = hamburger.classList.toggle('open');
      mobileMenu.classList.toggle('open', isOpen);
      hamburger.setAttribute('aria-expanded', String(isOpen));
      mobileMenu.setAttribute('aria-hidden', String(!isOpen));
    });

    // Fechar ao clicar num link do menu mobile
    mobileMenu.querySelectorAll('.nav__mobile-link, .btn').forEach(link => {
      link.addEventListener('click', () => {
        hamburger.classList.remove('open');
        mobileMenu.classList.remove('open');
        hamburger.setAttribute('aria-expanded', 'false');
        mobileMenu.setAttribute('aria-hidden', 'true');
      });
    });

    // Fechar ao clicar fora
    document.addEventListener('click', (e) => {
      if (!header.contains(e.target) && mobileMenu.classList.contains('open')) {
        hamburger.classList.remove('open');
        mobileMenu.classList.remove('open');
        hamburger.setAttribute('aria-expanded', 'false');
        mobileMenu.setAttribute('aria-hidden', 'true');
      }
    });
  }

  /* ---- FILTRO DE PRODUTOS ---- */
  const filterBtns = document.querySelectorAll('.prod-filter');
  const prodCards  = document.querySelectorAll('.prod-card');

  if (filterBtns.length && prodCards.length) {
    filterBtns.forEach(btn => {
      btn.addEventListener('click', () => {
        const filter = btn.dataset.filter;

        // Atualiza estado dos botões
        filterBtns.forEach(b => {
          b.classList.remove('active');
          b.setAttribute('aria-selected', 'false');
        });
        btn.classList.add('active');
        btn.setAttribute('aria-selected', 'true');

        // Filtra os cards
        prodCards.forEach(card => {
          const show = filter === 'all' || card.dataset.cat === filter;
          card.style.display = show ? '' : 'none';

          // Reanima ao mostrar
          if (show) {
            card.classList.remove('visible');
            requestAnimationFrame(() => {
              requestAnimationFrame(() => card.classList.add('visible'));
            });
          }
        });
      });
    });
  }

  /* ---- ANIMAÇÕES DE ENTRADA (IntersectionObserver) ---- */
  const animEls = document.querySelectorAll('[data-animate]');

  if ('IntersectionObserver' in window && animEls.length) {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry, i) => {
        if (entry.isIntersecting) {
          // Pequeno delay escalonado para elementos na mesma seção
          const delay = Math.min(i * 60, 300);
          setTimeout(() => entry.target.classList.add('visible'), delay);
          observer.unobserve(entry.target);
        }
      });
    }, {
      threshold: 0.12,
      rootMargin: '0px 0px -40px 0px'
    });

    animEls.forEach(el => observer.observe(el));
  } else {
    // Fallback sem IO
    animEls.forEach(el => el.classList.add('visible'));
  }

  /* ---- SMOOTH SCROLL nos links de âncora ---- */
  document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', (e) => {
      const targetId = anchor.getAttribute('href');
      if (targetId === '#') return;

      const target = document.querySelector(targetId);
      if (!target) return;

      e.preventDefault();
      const headerH = header ? header.offsetHeight : 64;
      const top = target.getBoundingClientRect().top + window.scrollY - headerH - 8;

      window.scrollTo({ top, behavior: 'smooth' });
    });
  });

  /* ---- NAV LINK ATIVO conforme scroll ---- */
  const sections    = document.querySelectorAll('section[id]');
  const navLinks    = document.querySelectorAll('.nav__link');
  const headerH     = () => (header ? header.offsetHeight : 64);

  if (sections.length && navLinks.length) {
    const setActive = () => {
      const scrollY = window.scrollY + headerH() + 32;
      let current = '';

      sections.forEach(sec => {
        if (scrollY >= sec.offsetTop) current = sec.id;
      });

      navLinks.forEach(link => {
        const href = link.getAttribute('href').replace('#', '');
        link.classList.toggle('active', href === current);
      });
    };

    window.addEventListener('scroll', setActive, { passive: true });
    setActive();
  }

})();
