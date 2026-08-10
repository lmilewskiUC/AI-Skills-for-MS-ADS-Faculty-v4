<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="https://fonts.googleapis.com/css2?family=EB+Garamond:ital,wght@0,400;0,600;1,400&family=Inter:wght@300;400;500;700&display=swap" rel="stylesheet">
<style>
:root {
  --maroon: #800000;
  --maroon-light: #fcf8f8;
  --gold: #EAAA00;
  --gold-text: #7a5200;
  --gray-border: #D9D9D9;
  --gray-mid: #A6A6A6;
  --gray-dark: #737373;
  --font-sans: 'Inter', Helvetica, Arial, sans-serif;
  --font-serif: 'EB Garamond', Georgia, serif;
}
* { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: var(--font-sans); background: #fff; color: #222; line-height: 1.5; }

.brand-header { background: var(--maroon); padding: 1.1rem 2rem; display: flex; align-items: center; gap: 1rem; }
.brand-header svg { width: 24px; height: 24px; fill: white; flex-shrink: 0; }
.brand-header h1 { font-size: 18px; font-weight: 500; letter-spacing: 0.02em; color: white; }

.view { display: none; }
.view.active { display: block; }

.main { padding: 2rem; max-width: 960px; margin: 0 auto; }

.page-header { background: var(--maroon); padding: 1.5rem 2rem; }
.page-header-text h2 { font-family: var(--font-serif); font-size: 2rem; color: #fff; margin-bottom: 0.25rem; }
.page-header-text p { font-size: 14px; color: rgba(255,255,255,0.75); }

.domain-card { border: 1.5px solid var(--gray-border); border-radius: 8px; margin-bottom: 1rem; overflow: hidden; transition: box-shadow 0.2s; }
.domain-card:hover { box-shadow: 0 4px 14px rgba(0,0,0,0.07); }
.domain-card.open { border-color: var(--maroon); box-shadow: 0 4px 14px rgba(128,0,0,0.1); }
.domain-header { display: flex; align-items: center; gap: 1rem; padding: 1.1rem 1.25rem; cursor: pointer; user-select: none; background: #fff; transition: background 0.15s; }
.domain-card.open .domain-header { background: var(--maroon-light); }
.domain-num { font-size: 11px; font-weight: 700; color: #fff; background: var(--maroon); border-radius: 4px; padding: 2px 7px; flex-shrink: 0; letter-spacing: 0.04em; }
.domain-name { font-size: 15px; font-weight: 600; color: #111; flex: 1; }
.domain-meta { font-size: 12px; color: var(--gray-mid); flex-shrink: 0; }
.chevron { flex-shrink: 0; transition: transform 0.25s; color: var(--gray-mid); }
.domain-card.open .chevron { transform: rotate(180deg); }

.drawer { max-height: 0; overflow: hidden; transition: max-height 0.35s cubic-bezier(0.4,0,0.2,1); background: #fafafa; border-top: 0px solid var(--gray-border); }
.domain-card.open .drawer { max-height: 500px; border-top-width: 1px; }
.drawer-inner { padding: 1.25rem; }

.track { display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 10px; }

.skill { background: #fff; border: 1.5px solid var(--gray-border); border-top: 3px solid var(--maroon); border-radius: 6px; padding: 0.9rem; cursor: pointer; transition: border-color 0.2s, box-shadow 0.2s, background 0.2s; display: flex; flex-direction: column; gap: 0.4rem; }
.skill:hover { box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #f9f9f9; border-color: var(--maroon); }
.skill-step { font-size: 10px; color: var(--gray-mid); font-weight: 600; }
.skill-name { font-size: 12px; font-weight: 600; color: #111; flex: 1; }

/* DETAIL VIEW */
.detail-page-header { background: #800000; padding: 2rem 2rem 1.75rem; }
.detail-breadcrumb { font-size: 12px; color: rgba(255,255,255,0.65); margin-bottom: 0.4rem; }
.detail-title { font-family: var(--font-serif); font-size: 2.2rem; color: #fff; line-height: 1.2; margin-bottom: 1rem; }
.detail-meta { display: flex; align-items: center; gap: 12px; }
.step-badge { font-size: 11px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.05em; padding: 3px 9px; border-radius: 10px; background: rgba(255,255,255,0.18); color: #fff; }

.detail-body { padding: 2rem; max-width: 720px; margin: 0 auto; }

.detail-skill-chips { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 2.5rem; }
.detail-chip { font-size: 12px; font-weight: 600; padding: 6px 12px; border-radius: 20px; border: 1.5px solid var(--gray-border); background: #fff; color: var(--gray-dark); cursor: pointer; transition: border-color 0.2s, background 0.2s, color 0.2s; }
.detail-chip:hover { border-color: var(--maroon); color: var(--maroon); }
.detail-chip.active { background: var(--maroon); border-color: var(--maroon); color: #fff; }

.desc-block { font-family: var(--font-serif); font-size: 1.25rem; line-height: 1.8; color: #333; margin-bottom: 2.5rem; padding-bottom: 2rem; border-bottom: 1px solid var(--gray-border); }

.section { margin-bottom: 2rem; }
.section-header { display: flex; align-items: center; gap: 10px; margin-bottom: 0.85rem; }
.section-number { width: 24px; height: 24px; border-radius: 50%; background: #800000; color: #fff; font-size: 11px; font-weight: 700; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
.section-title { font-size: 11px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.1em; color: var(--gray-dark); }
.section-body { font-size: 15px; line-height: 1.75; background: var(--maroon-light); padding: 1.5rem; border-radius: 6px; border-left: 4px solid #800000; color: #222; }
.section-placeholder { font-size: 14px; line-height: 1.7; background: #f7f7f5; padding: 1.5rem; border-radius: 6px; border: 1.5px dashed var(--gray-border); color: var(--gray-mid); font-style: italic; }

.resource-link { display: block; background: #f7f7f5; padding: 1rem 1.25rem; border-radius: 6px; text-decoration: none; color: #800000; font-weight: 600; font-size: 14px; margin-bottom: 0.75rem; border: 1px solid var(--gray-border); transition: border-color 0.2s, background 0.2s; }
.resource-link:hover { border-color: #800000; background: var(--maroon-light); }
.resource-link small { display: block; color: var(--gray-dark); font-weight: 400; font-size: 12px; margin-bottom: 4px; }
.no-resources { font-size: 14px; color: #888; font-style: italic; }

.skill-nav { display: flex; justify-content: space-between; align-items: center; margin-top: 2.5rem; padding-top: 1.5rem; border-top: 1px solid var(--gray-border); gap: 1rem; }
.nav-btn { display: flex; align-items: center; gap: 6px; font-size: 13px; font-weight: 500; color: #800000; background: none; border: 1.5px solid var(--gray-border); border-radius: 6px; padding: 0.5rem 1rem; cursor: pointer; transition: border-color 0.2s, background 0.2s; max-width: 200px; }
.nav-btn:hover { border-color: #800000; background: var(--maroon-light); }
.nav-btn:disabled { opacity: 0.3; cursor: default; pointer-events: none; }
.nav-btn span { white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
</style>
</head>
<body>

<header class="brand-header">
  <svg viewBox="0 0 20 20"><path d="M10 2L12.5 7.5H18L13.5 11L15.5 17L10 13.5L4.5 17L6.5 11L2 7.5H7.5L10 2Z"/></svg>
  <h1>University of Chicago, MS-Applied Data Science</h1>
</header>

<!-- MAP VIEW -->
<div id="view-map" class="view active">

  <div class="page-header">
    <div class="page-header-text">
      <h2>AI Competency Development Map</h2>
      <p>Click any domain to expand its skills, then select a skill to view details.</p>
    </div>
  </div>

  <div class="main">
    <div id="map-root"></div>
  </div>

</div><!-- end view-map -->

<!-- DETAIL VIEW -->
<div id="view-detail" class="view">
  <div class="detail-page-header" id="detail-header"></div>
  <div class="detail-body" id="detail-content"></div>
</div>

<script>
const data = [
  {
    domain: "Create and Refine Learning Materials and Class Activities", num: "1",
    skills: [
      {
        id: "1.1", name: "Initial Creation of Materials Using AI",
        desc: "Use AI to generate new learning materials from scratch \u2014 slide decks, lecture notes, quizzes, exams, activities, labs, visuals, and more.",
        startHere: `AI tools can be leveraged to help build workshops and other class materials that previously took hours of instructor time to create. Instructors in the MS-ADS have used AI tools to generate datasets for practice, build machine learning models that students can test and critique, and even build simulations that allow students to investigate how imitation learning works. Try the AI Workshop Creation Guide below and take a look at some ways instructors have used AI to build new learning materials.`,
        tryItOut: [{t:"AI Workshop Creation Guide", type:"Activity", url: "https://canvas.uchicago.edu/courses/72214/pages/2-dot-3-plan-and-refine-class-activities-using-ai-try-it-out]"}],
        resources: [{t: "Sample Instructor AI Demo", url: "https://canvas.uchicago.edu/courses/72214/pages/2-dot-3-plan-and-execute-class-activities-instructor-demo-of-ai-tool-video", type: "Video"}, {t:"Sample Workshop Activity: Imitation Learning with Donkey Cars", url: "https://canvas.uchicago.edu/courses/72214/pages/2-dot-3-sample-workshop-francisco-azeredo-imitation-learning-using-donkey-car-simulator?module_item_id=3130218", type: "Student Handout"}, {t:`Collection: In-Class AI Workshop Ideas`, type:"Discussion Board", url: "https://canvas.uchicago.edu/courses/72558/discussion_topics/997908"}]
      },
      {
        id: "1.2", name: "Refinement of Materials Using AI",
        desc: "Refine existing learning artifacts (slide decks, lecture scripts, examples, assignments, etc.) using AI tools to improve clarity and organization of materials.",
        startHere: [], tryItOut: [], resources: []
      },
      {
        id: "1.3", name: "Updating Materials Using AI, Including Agentic Use",
        desc: "Keep materials current and aligned with course learning outcomes over time, using AI \u2014 including agentic AI tools that can autonomously identify and apply updates across a set of materials.",
        startHere: [], tryItOut: [], resources: []
      }
    ]
  },
  {
    domain: "Teach Students About Effective AI Use and Potential Pitfalls", num: "2",
    skills: [
      {
        id: "2.1", name: "Discipline-Specific AI Use and Pitfalls",
        desc: "Clearly explain and demonstrate the advantages and pitfalls of AI use within your specific content area.",
        startHere: `Most students today are using AI for all kinds of purposes in their schoolwork. What they need instructor support with most is understanding the ins and outs of using AI in the instructor's specific content area. In this skill, you'll build some AI demos that help students see how they can use AI to their advantage in your content area, while also avoiding the major pitfalls.`,
        tryItOut: [{t: `Plan an In-Class AI Demo`, type: "Activity", url: "https://canvas.uchicago.edu/courses/72214/pages/2-dot-2-advantages-and-pitfalls-of-ai-use-plan-a-demo"}],
        resources: [{t: `Statistical & Quantitative Hallucinations Video - Sebastien Donadio`, type: "Video", url: "https://canvas.uchicago.edu/courses/72214/pages/2-dot-2-advantages-and-pitfalls-of-ai-use-instructor-video"}, {t:`The Case for Memorization - Learning Curve Podcast`, type: "Podcast", url: "https://learningcurve.fm/episodes/the-case-for-memorization-in-the-ai-era/transcript"}]
      },
      {
        id: "2.2", name: "Professional AI Use (Presentations, etc.)",
        desc: "Teach students to use AI to support professional work such as revising papers and rehearsing presentations.",
        startHere: `Two examples to draw on when building this skill: Jonathan's Capstone example, where students use AI to get feedback and ideas for revising a paper, and using an AI persona to get feedback on a presentation before delivering it live.`,
        tryItOut: [], resources: []
      },
      {
        id: "2.3", name: "AI Use for Learning",
        desc: "Describe how you want students to use AI to accomplish or demonstrate a learning outcome, and help them apply AI effectively to learn and practice course content.",
        startHere: `The goal of this exercise is for you to clarify what you want students to be able to do using AI for various parts of your class. In the activity below, you will think through what the main skills and content are in your class and how students might use AI effectively or ineffectively to learn and implement them.`,
        tryItOut: [{t:"Learning Outcome Thought Partner", type:"AI Agent", url: "https://phoenixai.uchicago.edu/gpts/QEd3ErpGSK-diuwprISKEA"}, {t: "Breaking Down Learning Outcomes and AI Use", type: "Activity", url: "https://docs.google.com/document/d/1nM-BdbdiVyb665X1AHxvFykSIUhHYRFZgYJoIVD_02k/edit?tab=t.0#heading=h.8wnk5k4fbwp"}],
        resources: [{t: "AI Syllabus Statements", type: "Template", url: "https://canvas.uchicago.edu/courses/72558/files/15463877?module_item_id=3133071"}]
      },
      {
        id: "2.4", name: "Evaluating AI Tools",
        desc: "Teach students how to critically evaluate AI tools \u2014 their capabilities, limitations, and fit for a given task \u2014 rather than using whichever tool is most convenient.",
        startHere: [], tryItOut: [], resources: []
      }
    ]
  },
  {
    domain: "Leverage AI as an Instructional Assistant", num: "3",
    skills: [
      {
        id: "3.1", name: "Grading",
        desc: "Explain ethical and non-ethical uses of AI for grading, and use AI tools thoughtfully to support the grading process.",
        startHere: [], tryItOut: [], resources: []
      },
      {
        id: "3.2", name: "Tutoring",
        desc: "Teach students to use AI as an effective tutor for the course content, including ways to apply and test learning using AI tools.",
        startHere: [], tryItOut: [], resources: []
      },
      {
        id: "3.3", name: "Ethics",
        desc: "Explain ethical and non-ethical uses of AI for grading and tutoring, and set clear expectations for appropriate use.",
        startHere: [], tryItOut: [], resources: []
      }
    ]
  },
  {
    domain: "Stay Current on AI Use in Industry, Academia, and Education", num: "4",
    skills: [
      { id: "4.1", name: "Read and Process General AI News", desc: "Read and process information about new developments in AI generally.", startHere: [], tryItOut: [], resources: [] },
      { id: "4.2", name: "Read and Process Industry-Specific AI Developments", desc: "Read and process information about new developments in AI in your area of expertise and in education.", startHere: [], tryItOut: [], resources: [] },
      { id: "4.3", name: "Experiment with New AI Tools", desc: "Experiment with new AI tools for work and for teaching.", startHere: [], tryItOut: [], resources: [] },
      { id: "4.4", name: "Develop a Learning Practice and Share Your Learning", desc: "Cultivate a regular practice of learning and experimentation for new AI tools and developments, and share this with students and colleagues.", startHere: [], tryItOut: [], resources: [] }
    ]
  }
];

const allSkills = [];
data.forEach(d => d.skills.forEach(s => allSkills.push({ ...s, domainName: d.domain, domainNum: d.num, domainSkills: d.skills })));

document.addEventListener('DOMContentLoaded', function() {

const root = document.getElementById('map-root');
data.forEach((domain, di) => {
  const card = document.createElement('div');
  card.className = 'domain-card';
  card.id = `domain-${di}`;

  const trackHTML = domain.skills.map((s) => {
    return `<div class="skill" onclick="showDetail('${s.id}', event)">
      <div class="skill-step">${s.id}</div>
      <div class="skill-name">${s.name}</div>
    </div>`;
  }).join('');

  card.innerHTML = `
    <div class="domain-header" onclick="toggleDomain(${di})">
      <div class="domain-num">${domain.num}</div>
      <div class="domain-name">${domain.domain}</div>
      <div class="domain-meta">${domain.skills.length} skills</div>
      <svg class="chevron" width="16" height="16" viewBox="0 0 16 16" fill="none">
        <path d="M4 6l4 4 4-4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </div>
    <div class="drawer">
      <div class="drawer-inner"><div class="track">${trackHTML}</div></div>
    </div>
  `;
  root.appendChild(card);
});

}); // end DOMContentLoaded

window.toggleDomain = function(di) {
  const card = document.getElementById(`domain-${di}`);
  const isOpen = card.classList.contains('open');
  document.querySelectorAll('.domain-card').forEach(c => c.classList.remove('open'));
  if (!isOpen) card.classList.add('open');
};

function sectionHTML(num, title, items) {
  if (typeof items === 'string') {
    return `
      <div class="section">
        <div class="section-header">
          <div class="section-number">${num}</div>
          <div class="section-title">${title}</div>
        </div>
        <div class="section-body">${items}</div>
      </div>`;
  }

  const hasContent = items && items.length > 0;
  const bodyHTML = hasContent
    ? items.map(r => `
        <a href="${r.url || '#'}" target="${r.url && r.url !== '#' ? '_blank' : '_self'}" class="resource-link">
          <small>${r.type}</small>${r.t}
        </a>`).join('')
    : '<p class="no-resources">Content coming soon.</p>';

  return `
    <div class="section">
      <div class="section-header">
        <div class="section-number">${num}</div>
        <div class="section-title">${title}</div>
      </div>
      ${bodyHTML}
    </div>`;
}

window.showDetail = function(id, e) {
  if (e) e.stopPropagation();
  const globalIdx = allSkills.findIndex(s => s.id === id);
  const entry = allSkills[globalIdx];
  const domainSkills = entry.domainSkills;
  const localIdx = domainSkills.findIndex(s => s.id === id);

  const chips = domainSkills.map((s, i) =>
    `<button class="detail-chip ${i === localIdx ? 'active' : ''}" onclick="showDetail('${s.id}')">${s.name}</button>`
  ).join('');

  const prev = allSkills[globalIdx - 1];
  const next = allSkills[globalIdx + 1];

  const resourcesHTML = entry.resources && entry.resources.filter(r => r.t).length > 0
    ? entry.resources.filter(r => r.t).map(r => `
        <a href="${r.url||'#'}" target="${r.url && r.url !== '#' ? '_blank' : '_self'}" class="resource-link">
          <small>${r.type}</small>${r.t}
        </a>`).join('')
    : '<p class="no-resources">Resources for this skill are being curated by the department.</p>';

  document.getElementById('detail-header').innerHTML = `
    <button onclick="showMap()" style="display:inline-flex;align-items:center;gap:7px;background:#EAAA00;color:#7a5200;font-family:'Inter',sans-serif;font-size:13px;font-weight:700;border:none;border-radius:6px;padding:7px 14px;cursor:pointer;margin-bottom:1.25rem;">
      <svg width="14" height="14" viewBox="0 0 16 16" fill="none"><path d="M10 12L6 8l4-4" stroke="#7a5200" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
      Back to competency map
    </button>
    <div class="detail-breadcrumb">${entry.domainNum}. ${entry.domainName}</div>
    <div class="detail-title">${entry.name}</div>
    <div class="detail-meta">
      <span class="step-badge">Skill ${entry.id}</span>
    </div>
  `;

  document.getElementById('detail-content').innerHTML = `
    <div style="margin-bottom:0.5rem;margin-top:0.25rem;font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:0.08em;color:var(--gray-dark);">Other skills in this domain</div>
    <div class="detail-skill-chips">${chips}</div>
    <div class="desc-block">${entry.desc}</div>
    ${sectionHTML(1, 'Start Here', entry.startHere)}
    ${sectionHTML(2, 'Try It Out', entry.tryItOut)}
    <div class="section">
      <div class="section-header">
        <div class="section-number">3</div>
        <div class="section-title">Additional Resources</div>
      </div>
      ${resourcesHTML}
    </div>
    <div class="skill-nav">
      <button class="nav-btn" onclick="showDetail('${prev ? prev.id : ''}')" ${!prev ? 'disabled' : ''}>
        <svg width="14" height="14" viewBox="0 0 16 16" fill="none" style="flex-shrink:0"><path d="M10 12L6 8l4-4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg>
        <span>${prev ? prev.name : ''}</span>
      </button>
      <span style="font-size:12px;color:var(--gray-mid);white-space:nowrap;">${entry.id} of ${allSkills.length}</span>
      <button class="nav-btn" onclick="showDetail('${next ? next.id : ''}')" ${!next ? 'disabled' : ''}>
        <span>${next ? next.name : ''}</span>
        <svg width="14" height="14" viewBox="0 0 16 16" fill="none" style="flex-shrink:0"><path d="M6 4l4 4-4 4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg>
      </button>
    </div>
  `;

  document.getElementById('view-map').classList.remove('active');
  document.getElementById('view-detail').classList.add('active');
  window.scrollTo(0, 0);
};

window.showMap = function() {
  document.getElementById('view-detail').classList.remove('active');
  document.getElementById('view-map').classList.add('active');
};
</script>

<script>
  function resizeParent() {
    const height = document.body.scrollHeight;
    parent.postMessage({ subject: 'lti.frameResize', height: height }, '*');
  }
  window.addEventListener('load', resizeParent);
  window.addEventListener('resize', resizeParent);
  const observer = new MutationObserver(resizeParent);
  observer.observe(document.body, { childList: true, subtree: true, attributes: true });
</script>
</body>
</html>
