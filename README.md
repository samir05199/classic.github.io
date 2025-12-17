# classic.github.io
Classic Website


* script.js: useful interactions
  _______________________________________________________
js
// Run after DOM is ready
document.addEventListener('DOMContentLoaded', () => {
  // 1) Smooth scroll for nav links
  document.querySelectorAll('a[href^="#"]').forEach(link => {
    link.addEventListener('click', e => {
      const targetId = link.getAttribute('href');
      const targetEl = document.querySelector(targetId);
      if (!targetEl) return;

      e.preventDefault();
      targetEl.scrollIntoView({ behavior: 'smooth', block: 'start' });
    });
  });

  // 2) Scroll-reveal animation for sections
  const revealEls = document.querySelectorAll('.scroll-reveal');

  const observer = new IntersectionObserver(
    entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible');
          observer.unobserve(entry.target); // reveal once
        }
      });
    },
    { threshold: 0.15, rootMargin: '0px 0px -50px 0px' }
  );

  revealEls.forEach(el => observer.observe(el));

  // 3) Simple cursor follower
  const cursor = document.createElement('div');
  cursor.className = 'cursor-follower';
  document.body.appendChild(cursor);

  let x = window.innerWidth / 2;
  let y = window.innerHeight / 2;
  let targetX = x;
  let targetY = y;

  document.addEventListener('pointermove', e => {
    targetX = e.clientX;
    targetY = e.clientY;
  });

  function animateCursor() {
    const speed = 0.16; // lower = smoother
    x += (targetX - x) * speed;
    y += (targetY - y) * speed;
    cursor.style.transform = `translate3d(${x}px, ${y}px, 0)`;
    requestAnimationFrame(animateCursor);
  }

  animateCursor();
});
This uses document.querySelectorAll, addEventListener, and IntersectionObserver to build dynamic behavior without extra libraries, a pattern often recommended for simple interactive content.​

CSS required for effects
