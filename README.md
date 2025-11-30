<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Parth Kaklotar — Portfolio (recreated)</title>

  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600&display=swap" rel="stylesheet">

  <style>
    :root{
      --bg:#0b0b0c;
      --muted:#bdbdbd;
      --accent:#ff5858;
      --container:1100px;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family: 'Montserrat', system-ui, -apple-system, 'Segoe UI', Roboto, Arial;
      background:var(--bg);
      color:#fff;
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      line-height:1.6;
    }
    a{color:inherit;text-decoration:none}
    .wrap{max-width:var(--container);margin:0 auto;padding:40px 24px}

    /* nav */
    nav{position:fixed;right:24px;top:20px;z-index:50;display:flex;gap:18px}
    nav a{color:rgba(255,255,255,0.92);font-weight:600}

    /* hero */
    .hero{
      min-height:68vh;
      display:flex;align-items:center;
      padding-left:6vw;position:relative;overflow:hidden;
    }
    .hero::before{
      content:'';position:absolute;inset:0;z-index:0;
      background-image:url('https://images.unsplash.com/photo-1501785888041-af3ef285b470?q=80&w=2000&auto=format&fit=crop&crop=faces');
      background-size:cover;background-position:center;
      filter:grayscale(30%) brightness(35%);
    }
    .hero .content{position:relative;z-index:2;max-width:800px}
    h1{font-size:56px;margin:0 0 12px;font-weight:300}
    .sub{color:var(--muted);font-size:18px;margin-bottom:22px}
    .btn{background:var(--accent);padding:12px 20px;border-radius:6px;color:#fff;font-weight:700}

    /* sections */
    section{padding:72px 0;border-top:1px solid rgba(255,255,255,0.03)}
    h2{font-size:34px;margin:0 0 8px}
    .line{height:4px;width:64px;background:var(--accent);border-radius:4px;margin-bottom:18px}

    /* two-column project layout */
    .projects{display:grid;gap:36px}
    .project{display:grid;grid-template-columns:1fr 540px;gap:28px;align-items:center}
    .project .meta h3{margin:0 0 8px;font-size:24px}
    .project .meta p{color:var(--muted);margin:0 0 12px}
    .tech{color:var(--muted);margin-bottom:12px}
    .screenshot{background:#0f0f0f;padding:16px;border-radius:6px}
    .screenshot img{display:block;width:100%;height:auto}

    /* about */
    .about{display:flex;gap:40px;align-items:center}
    .avatar{width:220px;height:220px;border-radius:50%;overflow:hidden;border:8px solid rgba(255,255,255,0.04)}
    .avatar img{width:100%;height:100%;object-fit:cover}
    .about p{color:var(--muted);max-width:640px}

    /* contact form */
    form input, form textarea{width:100%;padding:12px;border-radius:8px;border:1px solid rgba(255,255,255,0.06);background:transparent;color:#fff}
    .muted{color:var(--muted)}

    /* responsive */
    @media (max-width:980px){
      h1{font-size:44px}
      .project{grid-template-columns:1fr 1fr}
    }
    @media (max-width:760px){
      nav{right:12px;top:12px}
      .project{grid-template-columns:1fr}
      .screenshot{order:-1}
      .about{flex-direction:column;align-items:flex-start}
      .avatar{width:180px;height:180px}
    }
  </style>
</head>
<body>

  <nav aria-label="main nav">
    <a href="#work">Work</a>
    <a href="#about">About</a>
    <a href="#contact">Contact</a>
  </nav>

  <header class="hero">
    <div class="content wrap">
      <h1>Parth Kaklotar</h1>
      <div class="sub">Computer Engineering student &amp; web developer — I build clean, responsive websites and small web apps.</div>
      <a class="btn" href="#contact">Get in touch</a>
    </div>
  </header>

  <main class="wrap">
    <section id="work">
      <h2>Projects</h2>
      <div class="line"></div>

      <div class="projects">
        <article class="project">
          <div class="meta">
            <h3>Personal Portfolio</h3>
            <p class="muted">A responsive portfolio showcasing projects, skills and contact details. Built with HTML, CSS &amp; JS.</p>
            <div class="tech">HTML • CSS • JavaScript • Responsive</div>
            <a href="#" class="muted">Visit Site →</a>
          </div>
          <div class="screenshot">
            <img src="https://images.unsplash.com/photo-1522202176988-66273c2fd55f?q=80&w=1200&auto=format&fit=crop" alt="portfolio screenshot">
          </div>
        </article>

        <article class="project">
          <div class="meta">
            <h3>Calculator App</h3>
            <p class="muted">Minimal JS calculator with keyboard support and clean UX.</p>
            <div class="tech">JavaScript • Accessibility</div>
            <a href="#" class="muted">Visit Site →</a>
          </div>
          <div class="screenshot">
            <img src="https://images.unsplash.com/photo-1515879218367-8466d910aaa4?q=80&w=1200&auto=format&fit=crop" alt="calculator">
          </div>
        </article>

        <article class="project">
          <div class="meta">
            <h3>Landing Page</h3>
            <p class="muted">Marketing-style landing page with responsive layout and subtle animations.</p>
            <div class="tech">HTML • CSS • JS</div>
            <a href="#" class="muted">Visit Site →</a>
          </div>
          <div class="screenshot">
            <img src="https://images.unsplash.com/photo-1507525428034-b723cf961d3e?q=80&w=1200&auto=format&fit=crop" alt="landing">
          </div>
        </article>
      </div>
    </section>

    <section id="about">
      <h2>About Me</h2>
      <div class="line"></div>

      <div class="about">
        <div class="avatar">
          <img src="https://images.unsplash.com/photo-1544005313-94ddf0286df2?q=80&w=800&auto=format&fit=crop" alt="parth avatar">
        </div>
        <div>
          <p class="muted">I’m Parth Kaklotar — a Computer Engineering student and web developer. I build clean, responsive websites and web apps. Currently pursuing a Diploma in Computer Engineering, I enjoy collaborating on projects and learning modern web technologies.</p>
          <p class="muted" style="margin-top:12px"><strong>Skills:</strong> HTML5, CSS3, JavaScript, Responsive Design, Git, VS Code</p>
          <a href="#" class="muted" style="display:inline-block;margin-top:12px">Download Resume</a>
        </div>
      </div>
    </section>

    <section id="contact">
      <h2>Contact</h2>
      <div class="line"></div>

      <p class="muted">Email: <a href="mailto:parthkaklotar544@gmail.com" class="muted">parthkaklotar544@gmail.com</a> · GitHub: <a href="https://github.com/parthkp126" class="muted">github.com/parthkp126</a></p>

      <form style="max-width:640px;margin-top:18px" id="contactForm">
        <label class="muted">Name</label>
        <input id="name" placeholder="Your name" required>
        <label class="muted" style="margin-top:10px;display:block">Message</label>
        <textarea id="message" rows="5" placeholder="Hi Parth..." required></textarea>
        <div style="margin-top:12px">
          <button class="btn" type="submit">Send message</button>
        </div>
      </form>
    </section>

  </main>

  <footer class="wrap" style="border-top:1px solid rgba(255,255,255,0.03);margin-top:40px;padding:30px 0;color:var(--muted)">
    © Parth Kaklotar — Built with ❤️
  </footer>

  <script>
    // Smooth scroll for internal anchor links
    document.querySelectorAll('a[href^="#"]').forEach(a=>{
      a.addEventListener('click', e=>{
        const target = document.querySelector(a.getAttribute('href'));
        if(target){ e.preventDefault(); target.scrollIntoView({behavior:'smooth', block:'start'}); }
      });
    });

    // Simple contact handler (demo only)
    document.getElementById('contactForm').addEventListener('submit', function(e){
      e.preventDefault();
      alert('Thanks! Message send demo. Replace this with real email / API.');
      this.reset();
    });
  </script>
</body>
</html>
