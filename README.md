```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Clinical Guideline: Suicidal Attempts by Jumping from Buildings</title>

  <!-- Essential CDN Libraries -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            // Inspired by playing cards - Hearts (red), Spades/Clubs (black), Diamonds (gold)
            heart: {
              50: '#fff5f5',
              100: '#fed7d7',
              200: '#feb2b2',
              300: '#fc8181',
              400: '#f56565',
              500: '#e53e3e',
              600: '#dd2c2c',
              700: '#c53030',
              800: '#9b2c2c',
              900: '#742a2a'
            },
            spade: {
              50: '#f7fafc',
              100: '#edf2f7',
              200: '#e2e8f0',
              300: '#cbd5e0',
              400: '#a0aec0',
              500: '#718096',
              600: '#4a5568',
              700: '#2d3748',
              800: '#1a202c',
              900: '#171923'
            },
            diamond: {
              50: '#fdf2f8',
              100: '#fce8f3',
              200: '#fbcfe8',
              300: '#f9a8d4',
              400: '#f472b6',
              500: '#ec4899',
              600: '#db2777',
              700: '#be185d',
              800: '#9d174d',
              900: '#831843'
            }
          },
          fontFamily: {
            'playing-card': ['"Playfair Display"', 'serif']
          }
        }
      }
    }
  </script>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;500;600;700&display=swap" rel="stylesheet">
  <script defer src="https://unpkg.com/alpinejs@3.x.x/dist/cdn.min.js"></script>
  <script src="https://unpkg.com/lucide@latest"></script>
  <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
  <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0"></script>

  <!-- Preline UI Components -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/preline@2.0.3/dist/preline.min.css">
  <script defer src="https://cdn.jsdelivr.net/npm/preline@2.0.3/dist/preline.js"></script>

  <!-- Custom Playing Card Inspired Styles -->
  <style>
    html { scroll-behavior: smooth; }

    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
      }
      html { scroll-behavior: auto; }
    }

    .btn-interactive {
      transition: all 0.2s ease-out;
      border: 2px solid transparent;
      position: relative;
      overflow: hidden;
    }
    
    .btn-interactive::before {
      content: '';
      position: absolute;
      top: 0;
      left: -100%;
      width: 100%;
      height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
      transition: left 0.5s;
    }
    
    .btn-interactive:hover::before {
      left: 100%;
    }
    
    .btn-interactive:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 20px -4px rgba(0, 0, 0, 0.15);
    }
    
    .btn-interactive:active {
      transform: translateY(0);
    }

    .card-playing {
      transition: all 0.3s ease-out;
      border: 2px solid transparent;
      background: white;
      position: relative;
      overflow: hidden;
      border-radius: 12px;
    }

    .card-playing::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: linear-gradient(135deg, rgba(255,255,255,0.1) 0%, rgba(255,255,255,0) 100%);
      z-index: 1;
    }

    .card-playing.heart-card {
      border-color: #e53e3e;
      box-shadow: 0 4px 12px rgba(229, 62, 62, 0.15);
    }

    .card-playing.diamond-card {
      border-color: #ec4899;
      box-shadow: 0 4px 12px rgba(236, 72, 153, 0.15);
    }

    .card-playing.spade-card {
      border-color: #4a5568;
      box-shadow: 0 4px 12px rgba(74, 85, 104, 0.15);
    }

    .card-playing:hover {
      transform: translateY(-4px);
      box-shadow: 0 12px 24px rgba(0, 0, 0, 0.15);
    }

    .playing-card-icon {
      font-size: 24px;
      line-height: 1;
      display: inline-block;
      margin-right: 8px;
      vertical-align: middle;
    }

    .heart-icon { color: #e53e3e; }
    .diamond-icon { color: #ec4899; }
    .spade-icon { color: #4a5568; }
    .club-icon { color: #4a5568; }

    .section-header {
      font-family: 'Playfair Display', serif;
      position: relative;
      padding-bottom: 12px;
    }

    .section-header::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 60px;
      height: 3px;
      background: linear-gradient(90deg, #e53e3e, #ec4899);
    }

    .dark .section-header::after {
      background: linear-gradient(90deg, #f56565, #f472b6);
    }

    .playing-card-pattern {
      position: absolute;
      opacity: 0.03;
      font-size: 48px;
      z-index: 0;
    }

    .pattern-heart { color: #e53e3e; }
    .pattern-diamond { color: #ec4899; }
    .pattern-spade { color: #4a5568; }
    .pattern-club { color: #4a5568; }

    body {
      background-image: 
        radial-gradient(circle at 10% 20%, rgba(229, 62, 62, 0.02) 0%, transparent 20%),
        radial-gradient(circle at 90% 80%, rgba(236, 72, 153, 0.02) 0%, transparent 20%),
        radial-gradient(circle at 50% 50%, rgba(74, 85, 104, 0.02) 0%, transparent 20%);
    }

    .dark body {
      background-image: 
        radial-gradient(circle at 10% 20%, rgba(245, 101, 101, 0.03) 0%, transparent 20%),
        radial-gradient(circle at 90% 80%, rgba(244, 114, 182, 0.03) 0%, transparent 20%),
        radial-gradient(circle at 50% 50%, rgba(113, 128, 150, 0.03) 0%, transparent 20%);
    }
  </style>

  <script>
    function toggleDarkMode() {
      document.body.classList.toggle('dark');
      const isDark = document.body.classList.contains('dark');
      document.getElementById('sunIcon').style.display = isDark ? 'block' : 'none';
      document.getElementById('moonIcon').style.display = isDark ? 'none' : 'block';
    }
  </script>
</head>

<body class="bg-gray-50 dark:bg-spade-900 text-spade-900 dark:text-spade-100 transition-colors duration-300 min-h-screen">
  <!-- Citation System Script -->
  <script>
    function initCitationSystem() {
      let i = 1, map = new Map();
      document.querySelectorAll('[data-ref]').forEach(el => {
        if (el.dataset.citationProcessed) return;
        const raw = (el.getAttribute('data-ref')||'').trim();
        if (!raw) return;

        const parts = raw.split('|');
        const url = parts[0].trim();
        const idx = (parts[1]||'').trim() || map.get(raw) || (map.set(raw, String(i)), String(i++));

        if (!el.textContent || !el.textContent.trim()) { el.dataset.citationProcessed = 'true'; return; }

        const btn = document.createElement('sup'); btn.textContent = String(idx);
        Object.assign(btn.style, { fontSize:'8px', color:'#fff', cursor:'pointer', top: '1px', fontWeight:'bold', backgroundColor:'#e53e3e', borderRadius:'50%', transition:'all .15s', userSelect:'none', minWidth:'19px', height:'19px', marginLeft:'6px', display:'inline-flex', alignItems:'center', justifyContent:'center', boxShadow:'0 1px 3px rgba(0,0,0,.2)', lineHeight:'1'});
        btn.addEventListener('mouseenter', ()=> Object.assign(btn.style, { backgroundColor:'#c53030', transform:'scale(1.12)' }));
        btn.addEventListener('mouseleave', ()=> Object.assign(btn.style, { backgroundColor:'#e53e3e', transform:'scale(1)' }));
        btn.addEventListener('click', e=>{ e.preventDefault(); e.stopPropagation(); window.open(url, '_blank'); });

        el.appendChild(btn); el.dataset.citationProcessed = 'true';
      });
    }
  </script>

  <!-- Progress bar with playing card theme -->
  <div class="fixed top-0 left-0 h-1 bg-gradient-to-r from-heart-500 via-diamond-500 to-heart-500 dark:from-heart-400 dark:via-diamond-400 dark:to-heart-400 z-[60] transition-all duration-300 ease-out" id="progressBar"></div>

  <!-- Floating Header with Playing Card Design -->
  <header class="fixed top-0 left-0 right-0 z-50 backdrop-blur bg-white/90 dark:bg-spade-900/90 border-b-2 border-heart-500 dark:border-heart-400">
    <nav class="max-w-7xl mx-auto px-6 py-4">
      <div class="flex items-center justify-between">
        <h1 class="text-xl font-bold text-spade-800 dark:text-spade-200 font-playing-card">
          <span class="heart-icon">♥</span> Clinical Guideline: Suicidal Attempts
        </h1>
        
        <div class="flex items-center gap-3 flex-wrap">
          <a href="#home" class="btn-interactive px-3 py-1.5 text-sm rounded-lg bg-heart-50 dark:bg-heart-900/30 text-heart-700 dark:text-heart-300 hover:bg-heart-100 dark:hover:bg-heart-800 border-heart-300 dark:border-heart-700 font-playing-card">Home</a>
          <a href="#definition" class="btn-interactive px-3 py-1.5 text-sm rounded-lg bg-diamond-50 dark:bg-diamond-900/30 text-diamond-700 dark:text-diamond-300 hover:bg-diamond-100 dark:hover:bg-diamond-800 border-diamond-300 dark:border-diamond-700 font-playing-card">Definition</a>
          <a href="#causes" class="btn-interactive px-3 py-1.5 text-sm rounded-lg bg-spade-50 dark:bg-spade-800 text-spade-700 dark:text-spade-300 hover:bg-spade-100 dark:hover:bg-spade-700 border-spade-300 dark:border-spade-600 font-playing-card">Causes</a>
          <a href="#assessment" class="btn-interactive px-3 py-1.5 text-sm rounded-lg bg-heart-50 dark:bg-heart-900/30 text-heart-700 dark:text-heart-300 hover:bg-heart-100 dark:hover:bg-heart-800 border-heart-300 dark:border-heart-700 font-playing-card">Assessment</a>
          <a href="#investigations" class="btn-interactive px-3 py-1.5 text-sm rounded-lg bg-diamond-50 dark:bg-diamond-900/30 text-diamond-700 dark:text-diamond-300 hover:bg-diamond-100 dark:hover:bg-diamond-800 border-diamond-300 dark:border-diamond-700 font-playing-card">Investigations</a>
          <a href="#differential" class="btn-interactive px-3 py-1.5 text-sm rounded-lg bg-spade-50 dark:bg-spade-800 text-spade-700 dark:text-spade-300 hover:bg-spade-100 dark:hover:bg-spade-700 border-spade-300 dark:border-spade-600 font-playing-card">Differential</a>
          <a href="#interactions" class="btn-interactive px-3 py-1.5 text-sm rounded-lg bg-heart-50 dark:bg-heart-900/30 text-heart-700 dark:text-heart-300 hover:bg-heart-100 dark:hover:bg-heart-800 border-heart-300 dark:border-heart-700 font-playing-card">Interactions</a>
          <a href="#conclusion" class="btn-interactive px-3 py-1.5 text-sm rounded-lg bg-diamond-50 dark:bg-diamond-900/30 text-diamond-700 dark:text-diamond-300 hover:bg-diamond-100 dark:hover:bg-diamond-800 border-diamond-300 dark:border-diamond-700 font-playing-card">Conclusion</a>
          
          <button onclick="toggleDarkMode()" class="btn-interactive p-2 rounded-lg bg-spade-100 dark:bg-spade-800 text-spade-600 dark:text-spade-300 hover:bg-spade-200 dark:hover:bg-spade-700 border-spade-300 dark:border-spade-600">
            <i data-lucide="sun" id="sunIcon" class="w-5 h-5" style="display:none;"></i>
            <i data-lucide="moon" id="moonIcon" class="w-5 h-5" style="display:block;"></i>
          </button>
        </div>
      </div>
    </nav>
  </header>

  <!-- Main Content -->
  <main class="min-h-screen pt-20">
    <!-- Hero Section with Playing Card Theme -->
    <section id="home" class="py-32 bg-gradient-to-br from-heart-50/30 via-diamond-50/30 to-spade-50/30 dark:from-heart-900/10 dark:via-diamond-900/10 dark:to-spade-900/10 relative overflow-hidden" data-aos="fade-up">
      <div class="playing-card-pattern pattern-heart top-10 left-10">♥</div>
      <div class="playing-card-pattern pattern-diamond top-20 right-20">♦</div>
      <div class="playing-card-pattern pattern-spade bottom-20 left-20">♠</div>
      <div class="playing-card-pattern pattern-club bottom-10 right-10">♣</div>
      
      <div class="max-w-5xl mx-auto px-6 relative z-10">
        <h2 class="text-4xl md:text-5xl font-bold mb-6 text-spade-800 dark:text-spade-200 font-playing-card">
          <span class="heart-icon">♥</span> Clinical Guideline for Suicidal Attempts by Jumping
        </h2>
        
        <div class="grid md:grid-cols-2 gap-8 items-start">
          <div class="space-y-4">
            <p class="text-spade-700 dark:text-spade-300 text-lg leading-relaxed font-playing-card">
              This comprehensive clinical guideline addresses the complex medical and psychiatric management of patients who have attempted suicide by jumping from buildings or heights. The guideline covers definition, causation, assessment protocols, investigations, differential diagnosis, and critical drug interactions relevant to both adult and pediatric populations.
            </p>

            <div class="pl-4 pr-3 py-3 border-l-4 border-heart-500 bg-heart-50/40 dark:bg-heart-900/30 rounded-r-lg">
              <p class="text-sm font-medium text-heart-900 dark:text-heart-100 leading-relaxed font-playing-card">
                <span class="heart-icon">♥</span> Jumping from a height represents a high-lethality suicide method with unique trauma patterns requiring specialized medical and psychiatric intervention.
              </p>
            </div>
          </div>

          <img
            src="https://cdn.qwenlm.ai/c71f8425-dcbc-4db1-9e1c-8c7744ff7fa5/cb6f10f2-c586-4973-abaa-a9f3be2292d7/9dc6713f-27cd-40e0-8161-d31b38187cfb.png?key=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyZXNvdXJjZV91c2VyX2lkIjoiYzcxZjg0MjUtZGNiYy00ZGIxLTllMWMtOGM3NzQ0ZmY3ZmE1IiwicmVzb3VyY2VfaWQiOiJjYjZmMTBmMi1jNTg2LTQ5NzMtYWJhYS1hOWYzYmUyMjkyZDciLCJyZXNvdXJjZV9jaGF0X2lkIjpudWxsfQ.yhMPYGiliRkP_XM5OP-EP6qTS-c5xmpSBaSG3njzer0"
            alt="Medical illustration showing a multi-story building with a red emergency medical services vehicle parked below. The scene depicts a clinical environment with medical personnel in blue scrubs attending to a patient on a stretcher. Surrounding the building are medical equipment silhouettes including an IV drip bag, stethoscope, and ECG monitor displaying waveforms. The background uses a calming blue-green gradient transitioning from light blue at the top to teal at the bottom. The composition includes subtle medical symbols like a caduceus and heart monitor icons positioned strategically around the building. All elements are rendered in a professional medical illustration style with clean lines and muted tones to emphasize the clinical nature of the subject matter."
            class="w-full rounded-xl shadow-lg hover:shadow-2xl transition-shadow duration-300 border-2 border-heart-300 dark:border-heart-700"
          />
        </div>
      </div>
    </section>

    <!-- Definition Section - Heart Theme -->
    <section id="definition" class="py-20 bg-white/80 dark:bg-spade-900 relative overflow-hidden" data-aos="fade-up">
      <div class="playing-card-pattern pattern-heart top-10 left-10 opacity-5">♥</div>
      <div class="playing-card-pattern pattern-heart bottom-10 right-10 opacity-5">♥</div>
      
      <div class="max-w-5xl mx-auto px-6 relative z-10">
        <h2 class="text-3xl font-bold mb-8 text-heart-700 dark:text-heart-300 section-header font-playing-card">
          <span class="heart-icon">♥</span> Definition and Classification
        </h2>

        <div class="space-y-6">
          <div class="card-playing heart-card p-6 bg-white/90 backdrop-blur-sm dark:bg-spade-800 rounded-xl shadow-md">
            <h3 class="text-xl font-semibold text-heart-700 dark:text-heart-300 mb-4 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC7891495/|19">
              <span class="heart-icon">♥</span> Suicide Attempt Definition
            </h3>
            <p class="text-spade-700 dark:text-spade-300 leading-relaxed font-playing-card">
              A suicide attempt is defined as a non-fatal, self-directed, potentially injurious behavior with any intent to die as a result of the behavior. This definition emphasizes the importance of both the act itself and the intent behind it, distinguishing it from accidental injuries or non-suicidal self-harm.
            </p>
          </div>

          <div class="grid md:grid-cols-2 gap-6">
            <div class="card-playing heart-card p-6 bg-heart-50/50 dark:bg-heart-900/20 rounded-xl shadow-md">
              <h3 class="text-lg font-semibold text-heart-700 dark:text-heart-300 mb-3 font-playing-card" data-ref="https://www.msdmanuals.com/professional/psychiatric-disorders/suicidal-behavior/suicidal-behavior|20">
                <span class="heart-icon">♥</span> Key Components
              </h3>
              <ul class="space-y-2 text-spade-700 dark:text-spade-300 text-sm font-playing-card">
                <li class="flex items-start">
                  <span class="heart-icon">♥</span>
                  <span><strong>Suicidal ideation:</strong> Process of thinking about, considering, or planning suicide</span>
                </li>
                <li class="flex items-start">
                  <span class="heart-icon">♥</span>
                  <span><strong>Suicidal intent:</strong> Intention to end one's life through suicide</span>
                </li>
                <li class="flex items-start">
                  <span class="heart-icon">♥</span>
                  <span><strong>Suicide attempt:</strong> Non-fatal, self-directed behavior with intent to die</span>
                </li>
              </ul>
            </div>

            <div class="card-playing heart-card p-6 bg-heart-50/50 dark:bg-heart-900/20 rounded-xl shadow-md">
              <h3 class="text-lg font-semibold text-heart-700 dark:text-heart-300 mb-3 font-playing-card" data-ref="https://www.frontiersin.org/journals/psychiatry/articles/10.3389/fpsyt.2024.1278230/full|21">
                <span class="heart-icon">♥</span> Suicidal Behavior Disorder (SBD)
              </h3>
              <p class="text-spade-700 dark:text-spade-300 text-sm leading-relaxed font-playing-card">
                SBD is characterized by a self-initiated sequence of behaviors believed at the time of initiation to cause one's own death and occurring in the last
                <span class="mx-1 px-1.5 py-0.5 rounded-md bg-heart-100 dark:bg-heart-900/30 text-heart-800 dark:text-heart-300 font-semibold text-sm">24</span>
                hours.
              </p>
            </div>
          </div>

          <div class="pl-4 pr-3 py-3 border-l-4 border-amber-500 bg-amber-50/40 dark:bg-amber-900/30 rounded-r-lg">
            <p class="text-sm font-medium text-amber-900 dark:text-amber-100 leading-relaxed font-playing-card" data-ref="https://journals.sagepub.com/doi/10.1177/0706743716639054|26">
              <span class="heart-icon">♥</span> Important: The International Classification of Diseases (ICD) code for suicide attempts is W, with sensitivity of intentional self-harm defined by ICD-10 codes X60-X84 or Y87.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Causes Section - Diamond Theme -->
    <section id="causes" class="py-20 bg-gradient-to-br from-diamond-50/30 to-spade-50/30 dark:from-diamond-900/10 dark:to-spade-900/10 relative overflow-hidden" data-aos="fade-up">
      <div class="playing-card-pattern pattern-diamond top-20 left-20 opacity-5">♦</div>
      <div class="playing-card-pattern pattern-diamond bottom-20 right-20 opacity-5">♦</div>
      
      <div class="max-w-5xl mx-auto px-6 relative z-10">
        <h2 class="text-3xl font-bold mb-8 text-diamond-700 dark:text-diamond-300 section-header font-playing-card">
          <span class="diamond-icon">♦</span> Causes and Risk Factors
        </h2>

        <div class="space-y-6">
          <div class="grid md:grid-cols-2 gap-8 items-start">
            <div class="space-y-4">
              <h3 class="text-xl font-semibold text-diamond-700 dark:text-diamond-300 font-playing-card">
                <span class="diamond-icon">♦</span> Psychological and Social Factors
              </h3>
              
              <div class="card-playing diamond-card p-5 bg-white/90 backdrop-blur-sm dark:bg-spade-900 rounded-xl shadow-md">
                <h4 class="text-base font-semibold text-diamond-600 dark:text-diamond-400 mb-3 font-playing-card" data-ref="https://www.psychiatrist.com/pcc/serious-suicide-attempts-assessment-management/|31">
                  <span class="diamond-icon">♦</span> Psychiatric Illness Prevalence
                </h4>
                <p class="text-spade-700 dark:text-spade-300 text-sm leading-relaxed font-playing-card">
                  Those at highest risk for suicide are those with a psychiatric illness, with roughly
                  <span class="mx-1 px-1.5 py-0.5 rounded-md bg-diamond-100 dark:bg-diamond-900/30 text-diamond-800 dark:text-diamond-300 font-semibold text-sm">95%</span>
                  of suicide completers having a psychiatric diagnosis.
                </p>
              </div>

              <div class="card-playing diamond-card p-5 bg-white/90 backdrop-blur-sm dark:bg-spade-900 rounded-xl shadow-md">
                <h4 class="text-base font-semibold text-diamond-600 dark:text-diamond-400 mb-3 font-playing-card" data-ref="https://srcd.onlinelibrary.wiley.com/doi/10.1002/sop2.30|28">
                  <span class="diamond-icon">♦</span> Rising Trends in Adolescents
                </h4>
                <p class="text-spade-700 dark:text-spade-300 text-sm leading-relaxed font-playing-card">
                  Adolescent deaths by suicide have been rising in the United States for the last
                  <span class="mx-1 px-1.5 py-0.5 rounded-md bg-diamond-100 dark:bg-diamond-900/30 text-diamond-800 dark:text-diamond-300 font-semibold text-sm">15 years</span>,
                  with an age-adjusted rate at
                  <span class="mx-1 px-1.5 py-0.5 rounded-md bg-diamond-100 dark:bg-diamond-900/30 text-diamond-800 dark:text-diamond-300 font-semibold text-sm">7 per 100,000</span>
                  adolescents.
                </p>
              </div>
            </div>

            <img
              src="https://cdn.qwenlm.ai/c71f8425-dcbc-4db1-9e1c-8c7744ff7fa5/cb6f10f2-c586-4973-abaa-a9f3be2292d7/b034af4f-9cbd-4c22-8af2-8b9d660d7a7a.png?key=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyZXNvdXJjZV91c2VyX2lkIjoiYzcxZjg0MjUtZGNiYy00ZGIxLTllMWMtOGM3NzQ0ZmY3ZmE1IiwicmVzb3VyY2VfaWQiOiJjYjZmMTBmMi1jNTg2LTQ5NzMtYWJhYS1hOWYzYmUyMjkyZDciLCJyZXNvdXJjZV9jaGF0X2lkIjpudWxsfQ.yhMPYGiliRkP_XM5OP-EP6qTS-c5xmpSBaSG3njzer0"
              alt="Psychological profile infographic showing a human brain silhouette rendered in gradient blue-teal colors from light blue at the top to deep teal at the bottom. The brain contains three circular icons arranged vertically: a red warning triangle symbol with black outline at the top, a yellow exclamation mark symbol with black outline in the middle, and a green checkmark symbol with black outline at the bottom. Surrounding the brain are three text labels in sans-serif font: 'Psychiatric Illness 95%' positioned to the upper right, 'Adolescent Suicide 15 Years' positioned to the middle right, and 'Age-Adjusted Rate 7/100,000' positioned to the lower right. The background features a subtle medical cross symbol in light gray. All elements are cleanly designed with professional medical illustration styling using a calm blue-green color palette."
              class="w-full rounded-xl shadow-lg hover:shadow-2xl transition-shadow duration-300 border-2 border-diamond-300 dark:border-diamond-700"
            />
          </div>

          <div class="hs-accordion-group space-y-4">
            <div class="hs-accordion card-playing spade-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-spade-200 dark:border-spade-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-spade-50 dark:hover:bg-spade-700/50 transition-colors rounded-xl" id="hs-causes-1">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-heart-100 dark:bg-heart-900/30 rounded-lg flex items-center justify-center">
                    <span class="heart-icon text-2xl">♥</span>
                  </div>
                  <span class="font-semibold text-lg text-spade-700 dark:text-spade-300 font-playing-card"><span class="heart-icon">♥</span> Neurobiological Factors</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-spade-600 dark:text-spade-400"></i>
              </button>
              <div id="hs-collapse-causes-1" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-causes-1">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.mdpi.com/2073-4409/10/10/2519|83">
                    Serotonin deficits are implicated in pathogenesis of depression and also in aggression, impulsivity, suicidal ideations, and suicide attempts. Serotonin plays a crucial role in regulating mood, impulse control, and emotional stability.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC8929755/|81">
                    Higher cortisol response differentiated a suicide attempt subgroup with high impulsive aggression. Aggression, impulsivity and inflammatory markers serve as risk factors for suicidal behavior, with cortisol dysregulation indicating HPA axis abnormalities.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC4832012/|243">
                    Blunted cortisol and cortisol responses to stress may underlie increased impulsive aggression in subjects at high risk for suicidal behavior, suggesting HPA axis dysfunction contributes to suicide vulnerability.
                  </p>
                </div>
              </div>
            </div>

            <div class="hs-accordion card-playing spade-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-spade-200 dark:border-spade-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-spade-50 dark:hover:bg-spade-700/50 transition-colors rounded-xl" id="hs-causes-2">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-diamond-100 dark:bg-diamond-900/30 rounded-lg flex items-center justify-center">
                    <span class="diamond-icon text-2xl">♦</span>
                  </div>
                  <span class="font-semibold text-lg text-spade-700 dark:text-spade-300 font-playing-card"><span class="diamond-icon">♦</span> Social and Environmental Factors</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-spade-600 dark:text-spade-400"></i>
              </button>
              <div id="hs-collapse-causes-2" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-causes-2">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC7217666/|85">
                    Early adversity and parental psychopathology are particularly prominent in those who make childhood suicide attempts, highlighting the intergenerational transmission of risk factors.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.researchgate.net/publication/363541497_Child_maltreatment_and_youth_suicide_risk_A_developmental_conceptual_model_and_implications_for_suicide_prevention|53">
                    Experiences of child abuse and neglect are risk factors for youth suicidal thoughts and behaviors. Suicide risk may emerge as a developmental pathway influenced by adverse childhood experiences.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.cambridge.org/core/journals/psychological-medicine/article/intergenerational-transmission-of-suicide-attempt_in_a-cohort-of-44-million-children/7F2B1529D702861111D6599015587824|193">
                    Parental suicide attempt was associated with children's own suicide attempts. Exposure during early developmental stages was associated with the highest rates, emphasizing critical periods for intervention.
                  </p>
                </div>
              </div>
            </div>

            <div class="hs-accordion card-playing spade-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-spade-200 dark:border-spade-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-spade-50 dark:hover:bg-spade-700/50 transition-colors rounded-xl" id="hs-causes-3">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-spade-100 dark:bg-spade-900/30 rounded-lg flex items-center justify-center">
                    <span class="spade-icon text-2xl">♠</span>
                  </div>
                  <span class="font-semibold text-lg text-spade-700 dark:text-spade-300 font-playing-card"><span class="spade-icon">♠</span> Means Availability</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-spade-600 dark:text-spade-400"></i>
              </button>
              <div id="hs-collapse-causes-3" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-causes-3">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC7039710/|38">
                    Jumping from a height is an uncommon but lethal means of suicide. Restricting access to means is an important universal or population-based approach to suicide prevention.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://onlinelibrary.wiley.com/doi/10.1111/sltb.13030|79">
                    Although the increase in high-rise buildings was associated with the risk of jumping suicide in older people (ages 25-44, 45-64, and ≥65 years), means restriction remains a critical prevention strategy.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pdfs.semanticscholar.org/3136/46a034924a6a5104b52b139ba2ec4a1aaa78.pdf|54">
                    Jumping from a high place is the most common method of suicide among Korean children and adolescents, indicating cultural and environmental factors influencing method choice.
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Assessment Section - Spade Theme -->
    <section id="assessment" class="py-20 bg-white/80 dark:bg-spade-900 relative overflow-hidden" data-aos="fade-up">
      <div class="playing-card-pattern pattern-spade top-10 left-10 opacity-5">♠</div>
      <div class="playing-card-pattern pattern-club bottom-10 right-10 opacity-5">♣</div>
      
      <div class="max-w-5xl mx-auto px-6 relative z-10">
        <h2 class="text-3xl font-bold mb-8 text-spade-700 dark:text-spade-300 section-header font-playing-card">
          <span class="spade-icon">♠</span> Assessment Protocols
        </h2>

        <div class="space-y-6">
          <div class="grid md:grid-cols-2 gap-6">
            <div class="card-playing spade-card p-6 bg-spade-50/50 dark:bg-spade-900/20 rounded-xl shadow-md">
              <h3 class="text-lg font-semibold text-spade-700 dark:text-spade-300 mb-4 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC4724471/|74">
                <span class="spade-icon">♠</span> Emergency Department Requirements
              </h3>
              <p class="text-spade-700 dark:text-spade-300 text-sm leading-relaxed font-playing-card">
                The Joint Commission requires suicide screening and assessment for patients with primary emotional or behavioral disorders or presenting symptoms, ensuring systematic identification of at-risk individuals.
              </p>
            </div>

            <div class="card-playing spade-card p-6 bg-spade-50/50 dark:bg-spade-900/20 rounded-xl shadow-md">
              <h3 class="text-lg font-semibold text-spade-700 dark:text-spade-300 mb-4 font-playing-card" data-ref="">
                <span class="spade-icon">♠</span> Primary Assessment Goals
              </h3>
              <p class="text-spade-700 dark:text-spade-300 text-sm leading-relaxed font-playing-card">
                Following a serious suicide attempt, the primary goal is medical stabilization, followed by assessing the reasons for the attempt and the risk for future attempts.
              </p>
            </div>
          </div>

          <div class="pl-4 pr-3 py-3 border-l-4 border-spade-500 bg-spade-50/40 dark:bg-spade-900/30 rounded-r-lg">
            <p class="text-sm font-medium text-spade-900 dark:text-spade-100 leading-relaxed font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC6884133/|124">
              <span class="spade-icon">♠</span> Critical finding: Assessment should include evaluation of current mental state, psychiatric history, family history, social supports, and risk factors for suicide.
            </p>
          </div>

          <div class="hs-accordion-group space-y-4">
            <div class="hs-accordion card-playing heart-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-heart-200 dark:border-heart-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-heart-50 dark:hover:bg-heart-700/50 transition-colors rounded-xl" id="hs-assessment-1">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-heart-100 dark:bg-heart-900/30 rounded-lg flex items-center justify-center">
                    <span class="heart-icon text-2xl">♥</span>
                  </div>
                  <span class="font-semibold text-lg text-spade-700 dark:text-spade-300 font-playing-card"><span class="heart-icon">♥</span> Risk Assessment Tools</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-spade-600 dark:text-spade-400"></i>
              </button>
              <div id="hs-collapse-assessment-1" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-assessment-1">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC7190447/|47">
                    The Columbia–Suicide Severity Rating Scale (C-SSRS) is freely available and designed to measure the severity of suicidal ideation and behavior. It has been validated for use in children ages 6 to 12 years.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC7974826/|125">
                    The C-SSRS should not replace a complete clinical evaluation. It may be employed as an initial screening to guide a clinician in suicide risk assessment.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC9811343/|212">
                    The C-SSRS Screen may be feasible to use in the actual management setting as an initial step before the clinical assessment of suicide risk.
                  </p>
                </div>
              </div>
            </div>

            <div class="hs-accordion card-playing diamond-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-diamond-200 dark:border-diamond-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-diamond-50 dark:hover:bg-diamond-700/50 transition-colors rounded-xl" id="hs-assessment-2">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-diamond-100 dark:bg-diamond-900/30 rounded-lg flex items-center justify-center">
                    <span class="diamond-icon text-2xl">♦</span>
                  </div>
                  <span class="font-semibold text-lg text-spade-700 dark:text-spade-300 font-playing-card"><span class="diamond-icon">♦</span> Physical Examination Priorities</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-spade-600 dark:text-spade-400"></i>
              </button>
              <div id="hs-collapse-assessment-2" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-assessment-2">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC12647248/|58">
                    Patients who have fallen from great height with suicidal intent present unique challenges, including delayed medical attention, injury patterns, and complex trauma requiring immediate stabilization.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.researchgate.net/publication/376439781_Management_of_a_Polytrauma_After_Suicide_Attempt_by_Jumping_from_Great_Height_-_Case_Report|62">
                    Polytrauma caused by fall from a great height has an effect on multiple systems and organs. For a correct and complete diagnosis, proper imaging and multidisciplinary approach is essential.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.researchgate.net/publication/370635325_Injury_distribution_and_severity_in_suicidal_versus_accidental_fall_from_heights_need_for_a_multifactorial_consideration|151">
                    In-hospital mortality was
                    <span class="mx-1 px-1.5 py-0.5 rounded-md bg-red-100 dark:bg-red-900/30 text-red-800 dark:text-red-300 font-semibold text-sm">20.5%</span>
                    in intentional jumpers versus
                    <span class="mx-1 px-1.5 py-0.5 rounded-md bg-red-100 dark:bg-red-900/30 text-red-800 dark:text-red-300 font-semibold text-sm">5.2%</span>
                    in accidental fallers, with jumpers having notably higher injury severity scores.
                  </p>
                </div>
              </div>
            </div>

            <div class="hs-accordion card-playing spade-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-spade-200 dark:border-spade-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-spade-50 dark:hover:bg-spade-700/50 transition-colors rounded-xl" id="hs-assessment-3">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-spade-100 dark:bg-spade-900/30 rounded-lg flex items-center justify-center">
                    <span class="spade-icon text-2xl">♠</span>
                  </div>
                  <span class="font-semibold text-lg text-spade-700 dark:text-spade-300 font-playing-card"><span class="spade-icon">♠</span> Medication History</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-spade-600 dark:text-spade-400"></i>
              </button>
              <div id="hs-collapse-assessment-3" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-assessment-3">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC12831457/|30">
                    Over half of the overdose cases in this study were associated with a history of psychiatric hospitalization, indicating that the risk of suicide attempts is significantly elevated in this population.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://onlinelibrary.wiley.com/doi/10.1155/jonm/4823915|32">
                    Overall, the suicide attempt group showed significantly higher exposure to psychotropic drugs (d = 0.85, 95% CI = 0.78–0.92), which represented a substantial difference in medication exposure.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://onlinelibrary.wiley.com/doi/full/10.1002/npr2.12492|123">
                    Psychiatrists assessed information such as the history of psychiatric treatment and recent methods of deliberate self-harm, as well as prescribed drugs within one month of the attempt.
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Investigations Section - Diamond Theme -->
    <section id="investigations" class="py-20 bg-gradient-to-br from-diamond-50/30 to-heart-50/30 dark:from-diamond-900/10 dark:to-heart-900/10 relative overflow-hidden" data-aos="fade-up">
      <div class="playing-card-pattern pattern-diamond top-20 left-20 opacity-5">♦</div>
      <div class="playing-card-pattern pattern-heart bottom-20 right-20 opacity-5">♥</div>
      
      <div class="max-w-5xl mx-auto px-6 relative z-10">
        <h2 class="text-3xl font-bold mb-8 text-diamond-700 dark:text-diamond-300 section-header font-playing-card">
          <span class="diamond-icon">♦</span> Investigations and Laboratory Studies
        </h2>

        <div class="space-y-6">
          <div class="grid md:grid-cols-2 gap-8 items-start">
            <div class="space-y-4">
              <h3 class="text-xl font-semibold text-diamond-700 dark:text-diamond-300 font-playing-card">
                <span class="diamond-icon">♦</span> Initial Laboratory Investigations
              </h3>
              
              <div class="card-playing diamond-card p-5 bg-white/90 backdrop-blur-sm dark:bg-spade-900 rounded-xl shadow-md">
                <h4 class="text-base font-semibold text-diamond-600 dark:text-diamond-400 mb-3 font-playing-card" data-ref="https://pdfcoffee.com/the-harriet-lane-handbook-twenty-first-edition-pdf-free.html|71">
                  <span class="diamond-icon">♦</span> Recommended Laboratory Tests
                </h4>
                <p class="text-spade-700 dark:text-spade-300 text-sm leading-relaxed font-playing-card">
                  Consider complete blood cell count, electrolytes, liver function tests, ammonia, lactate, and toxicology screen (serum and urine) for comprehensive metabolic assessment.
                </p>
              </div>

              <div class="card-playing diamond-card p-5 bg-white/90 backdrop-blur-sm dark:bg-spade-900 rounded-xl shadow-md">
                <h4 class="text-base font-semibold text-diamond-600 dark:text-diamond-400 mb-3 font-playing-card" data-ref="https://www.ncbi.nlm.nih.gov/sites/books/n/statpearls/article-406/|6">
                  <span class="diamond-icon">♦</span> Toxicology Screening Scope
                </h4>
                <p class="text-spade-700 dark:text-spade-300 text-sm leading-relaxed font-playing-card">
                  Substances commonly assessed include therapeutic medications, illicit drugs, and environmental or occupational toxins. Screening relies on immunoassay techniques and gas chromatography-mass spectrometry.
                </p>
              </div>
            </div>

            <div class="space-y-4">
              <h3 class="text-xl font-semibold text-diamond-700 dark:text-diamond-300 font-playing-card">
                <span class="diamond-icon">♦</span> Imaging Studies
              </h3>
              
              <div class="card-playing diamond-card p-5 bg-white/90 backdrop-blur-sm dark:bg-spade-900 rounded-xl shadow-md">
                <h4 class="text-base font-semibold text-diamond-600 dark:text-diamond-400 mb-3 font-playing-card" data-ref="https://www.scribd.com/document/866029608/ATLS-11thEdition-Course-Manual-Final-250521-233327|9">
                  <span class="diamond-icon">♦</span> Head CT Guidelines
                </h4>
                <p class="text-spade-700 dark:text-spade-300 text-sm leading-relaxed font-playing-card">
                  The 2023 American College of Emergency Physicians clinical policy reviewed the Canadian CT Head Rule, New Orleans Criteria, and NEXUS Head CT criteria for determining appropriate imaging protocols.
                </p>
              </div>

              <div class="card-playing diamond-card p-5 bg-white/90 backdrop-blur-sm dark:bg-spade-900 rounded-xl shadow-md">
                <h4 class="text-base font-semibold text-diamond-600 dark:text-diamond-400 mb-3 font-playing-card" data-ref="https://www.mdpi.com/2077-0383/14/21|61">
                  <span class="diamond-icon">♦</span> Advanced Imaging Modalities
                </h4>
                <p class="text-spade-700 dark:text-spade-300 text-sm leading-relaxed font-playing-card">
                  Multi-slice computed tomography and magnetic resonance imaging are essential for detecting occult injuries, particularly in cases of polytrauma from falls from height.
                </p>
              </div>
            </div>
          </div>

          <div class="pl-4 pr-3 py-3 border-l-4 border-amber-500 bg-amber-50/40 dark:bg-amber-900/30 rounded-r-lg">
            <p class="text-sm font-medium text-amber-900 dark:text-amber-100 leading-relaxed font-playing-card" data-ref="https://www.sciencedirect.com/science/article/pii/S0379073825004281|2">
              <span class="diamond-icon">♦</span> Important: Toxicology positive/negative refers to the detection of drugs (licit, illicit, and amphetamine), alcohol and carboxyhemoglobin in postmortem analysis, requiring careful interpretation in living patients.
            </p>
          </div>

          <div class="hs-accordion-group space-y-4">
            <div class="hs-accordion card-playing heart-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-heart-200 dark:border-heart-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-heart-50 dark:hover:bg-heart-700/50 transition-colors rounded-xl" id="hs-invest-1">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-heart-100 dark:bg-heart-900/30 rounded-lg flex items-center justify-center">
                    <span class="heart-icon text-2xl">♥</span>
                  </div>
                  <span class="font-semibold text-lg text-diamond-700 dark:text-diamond-300 font-playing-card"><span class="heart-icon">♥</span> Cardiac Monitoring</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-diamond-600 dark:text-diamond-400"></i>
              </button>
              <div id="hs-collapse-invest-1" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-invest-1">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC10581389/|11">
                    This research aimed at validating the content of an algorithm for the assessment, management and monitoring of drug-induced QTc prolongation in mental health practice, highlighting the importance of cardiac monitoring.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pubmed.ncbi.nlm.nih.gov/16944043/|232">
                    This article discusses the potential of particular psychotropic drugs to prolong the QTc interval in children, and examines other factors that may contribute to cardiac risk.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.cambridge.org/core/journals/bjpsych-advances/article/understanding-and-managing-cardiac-sideeffects-of-secondgeneration-antipsychotics-in-the-treatment-of-schizophrenia/B2B19AA8ADD041AC735603A442A052E3|13">
                    Prolongation of the QT interval during treatment with psychotropic medication is one of the most common reasons for referral to cardiology from psychiatry, emphasizing the need for baseline ECG monitoring.
                  </p>
                </div>
              </div>
            </div>

            <div class="hs-accordion card-playing spade-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-spade-200 dark:border-spade-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-spade-50 dark:hover:bg-spade-700/50 transition-colors rounded-xl" id="hs-invest-2">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-spade-100 dark:bg-spade-900/30 rounded-lg flex items-center justify-center">
                    <span class="spade-icon text-2xl">♠</span>
                  </div>
                  <span class="font-semibold text-lg text-diamond-700 dark:text-diamond-300 font-playing-card"><span class="spade-icon">♠</span> Advanced Neuroimaging</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-diamond-600 dark:text-diamond-400"></i>
              </button>
              <div id="hs-collapse-invest-2" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-invest-2">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://link.springer.com/article/10.1186/s40345-024-00340-z|185">
                    Some standard neuroimaging techniques used in cognitive neuroscience research include functional magnetic resonance imaging (fMRI), diffusion tensor imaging, and positron emission tomography.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC12194819/|184">
                    This systematic review explores the role of electroencephalography (EEG)-based cognitive biomarkers in improving the understanding, diagnosis, monitoring, and treatment of neurological conditions.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC12005210/|240">
                    This study explores differences in interhemispheric connectivity between major depressive disorder patients with and without suicidal ideation, aiming to identify imaging biomarkers for suicide risk.
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Differential Diagnosis Section - Spade Theme -->
    <section id="differential" class="py-20 bg-white/80 dark:bg-spade-900 relative overflow-hidden" data-aos="fade-up">
      <div class="playing-card-pattern pattern-spade top-10 left-10 opacity-5">♠</div>
      <div class="playing-card-pattern pattern-club bottom-10 right-10 opacity-5">♣</div>
      
      <div class="max-w-5xl mx-auto px-6 relative z-10">
        <h2 class="text-3xl font-bold mb-8 text-spade-700 dark:text-spade-300 section-header font-playing-card">
          <span class="spade-icon">♠</span> Differential Diagnosis
        </h2>

        <div class="space-y-6">
          <div class="card-playing spade-card p-6 bg-spade-50/50 dark:bg-spade-900/20 rounded-xl shadow-md">
            <h3 class="text-xl font-semibold text-spade-700 dark:text-spade-300 mb-4 font-playing-card" data-ref="https://www.researchgate.net/publication/397415746_Forensic_Differentiation_of_Accidental_and_Intentional_Falls_from_Height_A_Systematic_Review_of_Injury_Patterns_Severity_Scores_and_Classification_Indicators|60">
              <span class="spade-icon">♠</span> Forensic Differentiation Principles
            </h3>
            <p class="text-spade-700 dark:text-spade-300 leading-relaxed font-playing-card">
              This review identifies consistent forensic indicators that may assist in distinguishing accidental from intentional falls from height. Injury distribution patterns, trauma severity scores, and classification indicators are critical for accurate determination.
            </p>
          </div>

          <div class="grid md:grid-cols-2 gap-6">
            <div class="card-playing spade-card p-6 bg-white/90 backdrop-blur-sm dark:bg-spade-800 rounded-xl shadow-md">
              <h3 class="text-lg font-semibold text-spade-700 dark:text-spade-300 mb-4 font-playing-card" data-ref="https://www.researchgate.net/publication/376031331_Characteristics_of_fall-from-height_patients_a_retrospective_comparison_of_jumpers_and_fallers_using_a_multi-institutional_registry|113">
                <span class="spade-icon">♠</span> Injury Pattern Differences
              </h3>
              <p class="text-spade-700 dark:text-spade-300 text-sm leading-relaxed font-playing-card">
                There was a very substantial difference in the injury pattern after suicidal jump (
                <span class="mx-1 px-1.5 py-0.5 rounded-md bg-spade-100 dark:bg-spade-900/30 text-spade-800 dark:text-spade-300 font-semibold text-sm">26% head</span>,
                <span class="mx-1 px-1.5 py-0.5 rounded-md bg-spade-100 dark:bg-spade-900/30 text-spade-800 dark:text-spade-300 font-semibold text-sm">69% pelvis</span>,
                <span class="mx-1 px-1.5 py-0.5 rounded-md bg-spade-100 dark:bg-spade-900/30 text-spade-800 dark:text-spade-300 font-semibold text-sm">65% lower extremity</span>
                lesions) compared to accidental falls.
              </p>
            </div>

            <div class="card-playing spade-card p-6 bg-white/90 backdrop-blur-sm dark:bg-spade-800 rounded-xl shadow-md">
              <h3 class="text-lg font-semibold text-spade-700 dark:text-spade-300 mb-4 font-playing-card" data-ref="https://www.sciencedirect.com/science/article/abs/pii/S0020138396000836|108">
                <span class="spade-icon">♠</span> Common Injuries in Suicidal Falls
              </h3>
              <p class="text-spade-700 dark:text-spade-300 text-sm leading-relaxed font-playing-card">
                The most common injuries were fractures of the thoracic and lumbar spine (
                <span class="mx-1 px-1.5 py-0.5 rounded-md bg-spade-100 dark:bg-spade-900/30 text-spade-800 dark:text-spade-300 font-semibold text-sm">83.0%</span>
                ), highlighting the distinctive trauma patterns in intentional falls from height.
              </p>
            </div>
          </div>

          <div class="hs-accordion-group space-y-4">
            <div class="hs-accordion card-playing heart-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-heart-200 dark:border-heart-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-heart-50 dark:hover:bg-heart-700/50 transition-colors rounded-xl" id="hs-diff-1">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-heart-100 dark:bg-heart-900/30 rounded-lg flex items-center justify-center">
                    <span class="heart-icon text-2xl">♥</span>
                  </div>
                  <span class="font-semibold text-lg text-spade-700 dark:text-spade-300 font-playing-card"><span class="heart-icon">♥</span> Psychosis-Related Behaviors</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-spade-600 dark:text-spade-400"></i>
              </button>
              <div id="hs-collapse-diff-1" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-diff-1">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.sciencedirect.com/science/article/abs/pii/S0165178107002089|76">
                    Persons who jumped from heights in general were more likely to suffer from schizophrenia than those who used other methods, indicating the role of psychotic disorders in method selection.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pubmed.ncbi.nlm.nih.gov/20482416/|183">
                    A large proportion of the survivors of suicide attempts by jumping were diagnosed with a psychotic illness, which confirms an association between psychosis and this method of attempt.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.researchgate.net/publication/44611257_Suicide_attempts_by_jumping_and_psychotic_illness|264">
                    One in five (
                    <span class="mx-1 px-1.5 py-0.5 rounded-md bg-red-100 dark:bg-red-900/30 text-red-800 dark:text-red-300 font-semibold text-sm">19.4%</span>
                    ) of all survivors of a suicide attempt by jumping had an undiagnosed and untreated psychosis that was often characterized by command hallucinations or delusions.
                  </p>
                </div>
              </div>
            </div>

            <div class="hs-accordion card-playing diamond-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-diamond-200 dark:border-diamond-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-diamond-50 dark:hover:bg-diamond-700/50 transition-colors rounded-xl" id="hs-diff-2">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-diamond-100 dark:bg-diamond-900/30 rounded-lg flex items-center justify-center">
                    <span class="diamond-icon text-2xl">♦</span>
                  </div>
                  <span class="font-semibold text-lg text-spade-700 dark:text-spade-300 font-playing-card"><span class="diamond-icon">♦</span> Accidental Falls vs. Intentional Attempts</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-spade-600 dark:text-spade-400"></i>
              </button>
              <div id="hs-collapse-diff-2" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-diff-2">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://doi.org/10.1016/j.forsciint.2026.112815|112">
                    Falls from height represent one of the leading causes of unintentional injury and death worldwide. Distinguishing between accidental, suicidal, and homicidal falls requires comprehensive forensic analysis.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.mdpi.com/2077-0383/14/17/6305|109">
                    While specific injuries may be characteristic of fatal free falls, they are not pathognomonic; similar injury patterns can also occur in other forms of blunt force trauma, requiring careful clinical correlation.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://journals.lww.com/sjfm/fulltext/2025/01000/forensic_differentiation_of_accidental_and.2.aspx|110">
                    This systematic review seeks to combine findings from the last year about injury patterns, trauma severity, and classification methods to distinguish between accidental and intentional falls from height.
                  </p>
                </div>
              </div>
            </div>

            <div class="hs-accordion card-playing spade-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-spade-200 dark:border-spade-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-spade-50 dark:hover:bg-spade-700/50 transition-colors rounded-xl" id="hs-diff-3">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-spade-100 dark:bg-spade-900/30 rounded-lg flex items-center justify-center">
                    <span class="spade-icon text-2xl">♠</span>
                  </div>
                  <span class="font-semibold text-lg text-spade-700 dark:text-spade-300 font-playing-card"><span class="spade-icon">♠</span> Catatonia and Delirium</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-spade-600 dark:text-spade-400"></i>
              </button>
              <div id="hs-collapse-diff-3" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-diff-3">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC12826656/|40">
                    We examined the effect of delirium and catatonia on psychosis symptom presentation in trauma intensive care unit patients without underlying psychiatric diagnoses, highlighting the importance of differential diagnosis.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://resolve.cambridge.org/core/services/aop-cambridge-core/content/view/078DDD946234BE11B27E15AE105E68FE/9780511543777c3_p33-70_CBO.pdf/the-many-faces-of-catatonia.pdf|42">
                    A review of the psychiatric manifestations in 108 patients with acute viral encephalitis finds delusions (
                    <span class="mx-1 px-1.5 py-0.5 rounded-md bg-diamond-100 dark:bg-diamond-900/30 text-diamond-800 dark:text-diamond-300 font-semibold text-sm">54%</span>
                    ), hallucinations (
                    <span class="mx-1 px-1.5 py-0.5 rounded-md bg-diamond-100 dark:bg-diamond-900/30 text-diamond-800 dark:text-diamond-300 font-semibold text-sm">44%</span>
                    ), mutism (
                    <span class="mx-1 px-1.5 py-0.5 rounded-md bg-diamond-100 dark:bg-diamond-900/30 text-diamond-800 dark:text-diamond-300 font-semibold text-sm">21%</span>
                    ), catalepsy (
                    <span class="mx-1 px-1.5 py-0.5 rounded-md bg-diamond-100 dark:bg-diamond-900/30 text-diamond-800 dark:text-diamond-300 font-semibold text-sm">15%</span>
                    ).
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://resolve.cambridge.org/core/services/aop-cambridge-core/content/view/0B4D4A51A1E316D56308065386DC41B1/9780511543777c4_p71-113_CBO.pdf/the-differential-diagnosis-of-catatonia.pdf|247">
                    The most likely cause of catatonia is a mood disorder. Exposure or withdrawal of psychoactive medicines, especially antipsychotic drugs, is another common cause requiring careful medication review.
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Drug Interactions Section - Heart Theme -->
    <section id="interactions" class="py-20 bg-gradient-to-br from-heart-50/30 to-diamond-50/30 dark:from-heart-900/10 dark:to-diamond-900/10 relative overflow-hidden" data-aos="fade-up">
      <div class="playing-card-pattern pattern-heart top-20 left-20 opacity-5">♥</div>
      <div class="playing-card-pattern pattern-diamond bottom-20 right-20 opacity-5">♦</div>
      
      <div class="max-w-5xl mx-auto px-6 relative z-10">
        <h2 class="text-3xl font-bold mb-8 text-heart-700 dark:text-heart-300 section-header font-playing-card">
          <span class="heart-icon">♥</span> Drug Interactions and Psychotropic Medications
        </h2>

        <div class="space-y-6">
          <div class="card-playing heart-card p-6 bg-white/90 backdrop-blur-sm dark:bg-spade-900 rounded-xl shadow-md">
            <h3 class="text-xl font-semibold text-heart-700 dark:text-heart-300 mb-4 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC12429776/|127">
              <span class="heart-icon">♥</span> Common Overdose Substances
            </h3>
            <p class="text-spade-700 dark:text-spade-300 leading-relaxed font-playing-card">
              In a review of more than 400,000 suicide attempts by drug overdose, opioids were implicated in
              <span class="mx-1 px-1.5 py-0.5 rounded-md bg-heart-100 dark:bg-heart-900/30 text-heart-800 dark:text-heart-300 font-semibold text-sm">47.8%</span>
              of fatal cases, followed by benzodiazepines and other substances.
            </p>
          </div>

          <div class="grid md:grid-cols-2 gap-6">
            <div class="card-playing heart-card p-6 bg-heart-50/50 dark:bg-heart-900/20 rounded-xl shadow-md">
              <h3 class="text-lg font-semibold text-heart-700 dark:text-heart-300 mb-4 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC8595792/|121">
                <span class="heart-icon">♥</span> Opioid-Benzodiazepine Interactions
              </h3>
              <p class="text-spade-700 dark:text-spade-300 text-sm leading-relaxed font-playing-card">
                This study examined whether prescription opioids and benzodiazepines interact to increase the rate of suicide attempt and intentional self-harm, highlighting the synergistic risk of combined use.
              </p>
            </div>

            <div class="card-playing diamond-card p-6 bg-diamond-50/50 dark:bg-diamond-900/20 rounded-xl shadow-md">
              <h3 class="text-lg font-semibold text-diamond-700 dark:text-diamond-300 mb-4 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC12171941/|271">
                <span class="diamond-icon">♦</span> Benzodiazepine-Specific Risk
              </h3>
              <p class="text-spade-700 dark:text-spade-300 text-sm leading-relaxed font-playing-card">
                There was a larger association for benzodiazepines with suicide attempt, intentional self-harm, and drug overdose, indicating elevated risk even when prescribed appropriately.
              </p>
            </div>
          </div>

          <div class="pl-4 pr-3 py-3 border-l-4 border-red-500 bg-red-50/40 dark:bg-red-900/30 rounded-r-lg">
            <p class="text-sm font-medium text-red-900 dark:text-red-100 leading-relaxed font-playing-card" data-ref="https://www.sciencedirect.com/science/article/abs/pii/S0022399919309821|161">
              <span class="heart-icon">♥</span> Critical finding: In this study, concomitant use of benzodiazepines and opioids was associated with a higher risk of death compared with use of a single drug, emphasizing the need for careful prescribing.
            </p>
          </div>

          <div class="hs-accordion-group space-y-4">
            <div class="hs-accordion card-playing spade-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-spade-200 dark:border-spade-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-spade-50 dark:hover:bg-spade-700/50 transition-colors rounded-xl" id="hs-interaction-1">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-spade-100 dark:bg-spade-900/30 rounded-lg flex items-center justify-center">
                    <span class="spade-icon text-2xl">♠</span>
                  </div>
                  <span class="font-semibold text-lg text-heart-700 dark:text-heart-300 font-playing-card"><span class="spade-icon">♠</span> QT Interval Prolongation</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-heart-600 dark:text-heart-400"></i>
              </button>
              <div id="hs-collapse-interaction-1" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-interaction-1">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.researchgate.net/publication/6680760_Cocaine_induced_prolongation_of_the_QT_interval|12">
                    Prolongation of the QT interval is a serious electrocardiogram finding because of its association with torsades de pointes and sudden cardiac death, requiring immediate clinical attention.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC12574724/|14">
                    ECG measurements should be taken at or near the drug's maximum daily blood concentration to ensure an accurate assessment of drug-induced QT interval prolongation.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pmc.ncbi.nlm.nih.gov/articles/PMC12373356/|241">
                    Antipsychotic drugs have the potential to cause QT-interval prolongation, which may lead to torsades de pointes and sudden cardiac death, necessitating routine ECG monitoring.
                  </p>
                </div>
              </div>
            </div>

            <div class="hs-accordion card-playing heart-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-heart-200 dark:border-heart-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-heart-50 dark:hover:bg-heart-700/50 transition-colors rounded-xl" id="hs-interaction-2">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-heart-100 dark:bg-heart-900/30 rounded-lg flex items-center justify-center">
                    <span class="heart-icon text-2xl">♥</span>
                  </div>
                  <span class="font-semibold text-lg text-heart-700 dark:text-heart-300 font-playing-card"><span class="heart-icon">♥</span> Akathisia and Suicidal Behavior</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-heart-600 dark:text-heart-400"></i>
              </button>
              <div id="hs-collapse-interaction-2" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-interaction-2">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pubmed.ncbi.nlm.nih.gov/34887662/|68">
                    Objective: We aim to systematically review evidence for a relationship between antipsychotic-induced akathisia and suicidal behavior, in order to guide clinical management.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.researchgate.net/publication/311694714_The_Mechanism_of_Drug-induced_Akathisia|128">
                    Akathisia is a movement disorder characterized by an inner sense of unease, unrest, and dysphoria. It can result in an inability to stand, sit, or lie still, potentially contributing to suicidal ideation.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.cambridge.org/core/journals/cns-spectrums/article/clinical-challenges-of-akathisia/666A3F2C382C7A928C5029703B11DD18|198">
                    Escitalopram-induced severe akathisia leading to suicide attempt highlights the importance of monitoring for movement disorder side effects in patients receiving psychotropic medications.
                  </p>
                </div>
              </div>
            </div>

            <div class="hs-accordion card-playing diamond-card bg-white/80 backdrop-blur-sm dark:bg-spade-800 rounded-xl border-2 border-diamond-200 dark:border-diamond-700">
              <button class="hs-accordion-toggle w-full flex justify-between items-center p-4 text-left hover:bg-diamond-50 dark:hover:bg-diamond-700/50 transition-colors rounded-xl" id="hs-interaction-3">
                <div class="flex items-center space-x-4">
                  <div class="flex-shrink-0 w-12 h-12 bg-diamond-100 dark:bg-diamond-900/30 rounded-lg flex items-center justify-center">
                    <span class="diamond-icon text-2xl">♦</span>
                  </div>
                  <span class="font-semibold text-lg text-heart-700 dark:text-heart-300 font-playing-card"><span class="diamond-icon">♦</span> Serotonin Syndrome</span>
                </div>
                <i data-lucide="chevron-down" class="hs-accordion-active:rotate-180 transition-transform duration-300 w-5 h-5 text-heart-600 dark:text-heart-400"></i>
              </button>
              <div id="hs-collapse-interaction-3" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300" aria-labelledby="hs-interaction-3">
                <div class="p-6 pt-0 space-y-4">
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.tandfonline.com/doi/pdf/10.1081/CLT-120022008|67">
                    Serotonin syndrome affects recipients of serotonergic drugs, especially in overdose or in combination. It comprises the rapid onset of altered mental status, autonomic instability, and neuromuscular abnormalities.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://pubmed.ncbi.nlm.nih.gov/38655989/|162">
                    Psychotropic recreational drug use is associated with suicidal ideation among adolescents regardless of current or previous use, abuse, or type of substance, indicating complex interactions.
                  </p>
                  <p class="text-spade-700 dark:text-spade-300 font-playing-card" data-ref="https://www.researchgate.net/publication/314174822_Prescribed_Benzodiazepines_and_Suicide_Risk_A_Review_of_the_Literature|122">
                    Treatment with medical drugs, such as hypnotics, has been associated with an increased risk of suicidal behavior, while they potentially also contribute to complex drug interactions.
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Conclusion Section - Mixed Theme -->
    <section id="conclusion" class="py-20 bg-white/80 dark:bg-spade-900 relative overflow-hidden" data-aos="fade-up">
      <div class="playing-card-pattern pattern-heart top-10 left-10 opacity-5">♥</div>
      <div class="playing-card-pattern pattern-diamond top-20 right-20 opacity-5">♦</div>
      <div class="playing-card-pattern pattern-spade bottom-20 left-20 opacity-5">♠</div>
      <div class="playing-card-pattern pattern-club bottom-10 right-10 opacity-5">♣</div>
      
      <div class="max-w-5xl mx-auto px-6 relative z-10">
        <h2 class="text-3xl font-bold mb-8 text-spade-700 dark:text-spade-300 section-header font-playing-card">
          <span class="heart-icon">♥</span> Conclusion and Clinical Recommendations
        </h2>

        <div class="space-y-6">
          <div class="card-playing spade-card p-6 bg-spade-50/50 dark:bg-spade-900/20 rounded-xl shadow-md">
            <h3 class="text-xl font-semibold text-spade-700 dark:text-spade-300 mb-4 font-playing-card">
              <span class="spade-icon">♠</span> Integrated Approach to Management
            </h3>
            <p class="text-spade-700 dark:text-spade-300 leading-relaxed font-playing-card">
              Managing suicidal attempts by jumping from buildings requires a comprehensive, multidisciplinary approach that integrates immediate medical stabilization, psychiatric assessment, and long-term risk mitigation. The high lethality and complex trauma patterns associated with this method necessitate specialized protocols for both adult and pediatric populations.
            </p>
          </div>

          <div class="grid md:grid-cols-2 gap-6">
            <div class="card-playing heart-card p-6 bg-white/90 backdrop-blur-sm dark:bg-spade-800 rounded-xl shadow-md">
              <h3 class="text-lg font-semibold text-heart-700 dark:text-heart-300 mb-4 font-playing-card">
                <span class="heart-icon">♥</span> Key Clinical Principles
              </h3>
              <ul class="space-y-3 text-spade-700 dark:text-spade-300 text-sm font-playing-card">
                <li class="flex items-start">
                  <span class="heart-icon">♥</span>
                  <span>Prioritize medical stabilization and trauma management</span>
                </li>
                <li class="flex items-start">
                  <span class="heart-icon">♥</span>
                  <span>Conduct comprehensive psychiatric assessment including risk factors</span>
                </li>
                <li class="flex items-start">
                  <span class="heart-icon">♥</span>
                  <span>Perform systematic investigations including toxicology and cardiac monitoring</span>
                </li>
                <li class="flex items-start">
                  <span class="heart-icon">♥</span>
                  <span>Differentiate intentional from accidental falls using forensic criteria</span>
                </li>
                <li class="flex items-start">
                  <span class="heart-icon">♥</span>
                  <span>Monitor for drug interactions, particularly QT prolongation and akathisia</span>
                </li>
              </ul>
            </div>

            <div class="card-playing diamond-card p-6 bg-white/90 backdrop-blur-sm dark:bg-spade-800 rounded-xl shadow-md">
              <h3 class="text-lg font-semibold text-diamond-700 dark:text-diamond-300 mb-4 font-playing-card">
                <span class="diamond-icon">♦</span> Prevention Strategies
              </h3>
              <ul class="space-y-3 text-spade-700 dark:text-spade-300 text-sm font-playing-card">
                <li class="flex items-start">
                  <span class="diamond-icon">♦</span>
                  <span>Implement means restriction through environmental modifications</span>
                </li>
                <li class="flex items-start">
                  <span class="diamond-icon">♦</span>
                  <span>Address early adversity and parental psychopathology in pediatric populations</span>
                </li>
                <li class="flex items-start">
                  <span class="diamond-icon">♦</span>
                  <span>Screen for psychiatric illness and provide timely interventions</span>
                </li>
                <li class="flex items-start">
                  <span class="diamond-icon">♦</span>
                  <span>Educate families about warning signs and help-seeking behaviors</span>
                </li>
                <li class="flex items-start">
                  <span class="diamond-icon">♦</span>
                  <span>Develop community-based crisis intervention programs</span>
                </li>
              </ul>
            </div>
          </div>

          <div class="pl-4 pr-3 py-3 border-l-4 border-spade-500 bg-spade-50/40 dark:bg-spade-900/30 rounded-r-lg">
            <p class="text-sm font-medium text-spade-900 dark:text-spade-100 leading-relaxed font-playing-card">
              <span class="heart-icon">♥</span> Future Directions: Continued research is needed to refine risk stratification tools, optimize treatment protocols, and evaluate the effectiveness of prevention interventions specifically targeting jumping as a suicide method.
            </p>
          </div>
        </div>
      </div>
    </section>
  </main>

  <!-- Footer with Playing Card Theme -->
  <footer class="bg-spade-900 dark:bg-spade-950 text-spade-100 dark:text-spade-300 py-12 relative overflow-hidden">
    <div class="playing-card-pattern pattern-heart top-10 left-10 opacity-10">♥</div>
    <div class="playing-card-pattern pattern-diamond top-20 right-20 opacity-10">♦</div>
    <div class="playing-card-pattern pattern-spade bottom-20 left-20 opacity-10">♠</div>
    <div class="playing-card-pattern pattern-club bottom-10 right-10 opacity-10">♣</div>
    
    <div class="max-w-5xl mx-auto px-6 relative z-10">
      <div class="grid md:grid-cols-3 gap-8">
        <div>
          <h3 class="text-lg font-semibold mb-4 text-spade-50 dark:text-spade-200 font-playing-card">
            <span class="heart-icon">♥</span> About This Guideline
          </h3>
          <p class="text-sm leading-relaxed font-playing-card">
            This comprehensive clinical guideline provides evidence-based recommendations for managing suicidal attempts by jumping from buildings, applicable to both adult and pediatric populations.
          </p>
        </div>
        
        <div>
          <h3 class="text-lg font-semibold mb-4 text-spade-50 dark:text-spade-200 font-playing-card">
            <span class="diamond-icon">♦</span> Key Topics
          </h3>
          <ul class="space-y-2 text-sm font-playing-card">
            <li>• <span class="heart-icon">♥</span> Definition and Classification</li>
            <li>• <span class="diamond-icon">♦</span> Causes and Risk Factors</li>
            <li>• <span class="spade-icon">♠</span> Assessment Protocols</li>
            <li>• <span class="diamond-icon">♦</span> Investigations and Testing</li>
            <li>• <span class="spade-icon">♠</span> Differential Diagnosis</li>
            <li>• <span class="heart-icon">♥</span> Drug Interactions</li>
          </ul>
        </div>
        
        <div>
          <h3 class="text-lg font-semibold mb-4 text-spade-50 dark:text-spade-200 font-playing-card">
            <span class="spade-icon">♠</span> Clinical Resources
          </h3>
          <ul class="space-y-2 text-sm font-playing-card">
            <li>• <span class="heart-icon">♥</span> Columbia-Suicide Severity Rating Scale</li>
            <li>• <span class="diamond-icon">♦</span> Emergency Department Protocols</li>
            <li>• <span class="spade-icon">♠</span> Toxicology Screening Guidelines</li>
            <li>• <span class="diamond-icon">♦</span> Cardiac Monitoring Standards</li>
            <li>• <span class="spade-icon">♠</span> Forensic Assessment Criteria</li>
          </ul>
        </div>
      </div>
      
      <div class="mt-8 pt-8 border-t border-spade-700 dark:border-spade-800 text-center text-sm font-playing-card">
        <p>&copy; 2024 Clinical Guideline Development. Educational resource for healthcare professionals.</p>
      </div>
    </div>
  </footer>

  <!-- Initialize Scripts -->
  <script>
    document.addEventListener('DOMContentLoaded', function() {
      // Initialize Lucide icons
      lucide.createIcons();

      // Initialize AOS animations
      AOS.init({
        duration: 800,
        once: true,
        offset: 100
      });

      // Progress bar functionality
      const progressBar = document.getElementById('progressBar');
      
      window.addEventListener('scroll', () => {
        const scrollTop = window.pageYOffset;
        const docHeight = document.body.scrollHeight - window.innerHeight;
        const scrollPercent = (scrollTop / docHeight) * 100;
        
        progressBar.style.width = scrollPercent + '%';
      });

      // Initialize citation system
      setTimeout(initCitationSystem, 100);

      // Initialize Preline components
      setTimeout(() => {
        document.dispatchEvent(new Event('preline:ready'));
      }, 100);
    });
  </script>
</body>
</html>
```
