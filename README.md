# Career-Planning-Resume-Builder-
Drag and Drop Resume Builder! Directions: Press on the skill cards on the left and drag them to the Resume categories on the right. You may add skill cards by typing in the blank and pressing add skill card. You are not required to use all skill cards in your resume. Once finished, press the button Print PDF and save. Then return to Edio.
<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Drag-and-Drop Resume Builder</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0; padding: 0;
      background-color: #f8f9fa;
    }
    h1 { text-align: center; margin: 20px 0; }
    .container {
      display: flex; justify-content: space-between;
      padding: 20px; gap: 20px;
    }
    .column {
      background: #fff; padding: 15px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      flex: 1;
    }
    .skills-list div {
      background-color: #d9f0f7;
      margin: 5px 0; padding: 10px;
      border-radius: 4px; cursor: grab;
    }
    .resume-section {
      border: 2px dashed #ccc;
      margin-bottom: 15px; padding: 10px;
    }
    .resume-section h3 { margin-top: 0; }
    .custom-inputs input {
      width: 100%; margin: 5px 0; padding: 8px;
    }
    .btn {
      display: inline-block;
      background-color: #28a745; color: #fff;
      padding: 10px 15px; border: none;
      border-radius: 4px; cursor: pointer;
      margin-top: 10px;
    }

    /* Optional: better page breaks if content grows */
    .page-break { page-break-before: always; break-before: page; }
  </style>

  <!-- ✅ Correct html2pdf bundle (includes html2canvas + jsPDF) -->
  <script defer src="https://cdn.jsdelivr.net/npm/html2pdf.js@0.10.1/dist/html2pdf.bundle.min.js"></script>
</head>
<body>
  <h1>Drag-and-Drop Resume Builder</h1>

  <div class="container">
    <!-- Left column: skill cards -->
    <div class="column">
      <h2>Skill Cards</h2>
      <div class="skills-list" id="skillsList">
        <div draggable="true">Good at following directions</div>
        <div draggable="true">Works well with others</div>
        <div draggable="true">Pays attention to detail</div>
        <div draggable="true">Technology enthusiast</div>
        <div draggable="true">Writes neatly and clearly</div>
        <div draggable="true">Microsoft Office skills</div>
        <div draggable="true">Enjoys working out</div>
        <div draggable="true">Enjoys volunteering</div>
        <div draggable="true">Human personality</div>
        <div draggable="true">Likes to read</div>
        <div draggable="true">High school graduate</div>
        <div draggable="true">Honor Roll Student</div>
        <div draggable="true">Volunteered at Community Center</div>
        <div draggable="true">Helped with School Events</div>
      </div>

      <h3>Add Your Own Ideas:</h3>
      <div class="custom-inputs">
        <input type="text" placeholder="Type your idea here" />
        <input type="text" placeholder="Type your idea here" />
        <input type="text" placeholder="Type your idea here" />
        <input type="text" placeholder="Type your idea here" />
        <button class="btn" type="button" onclick="addCustomSkills()">Add Skills</button>
      </div>
    </div>

    <!-- Right column: resume (export target) -->
    <div class="column" id="exportArea">
      <h2>Your Resume</h2>
      <div class="resume-section" id="skills"><h3>Skills</h3></div>
      <div class="resume-section" id="interests"><h3>Interests</h3></div>
      <div class="resume-section" id="education"><h3>Education</h3></div>
      <div class="resume-section" id="volunteer"><h3>Volunteer Work</h3></div>

      <button class="btn" type="button" onclick="downloadPDF()">Download as PDF</button>
    </div>
  </div>

  <script>
    const skillsList = document.getElementById('skillsList');
    const sections = document.querySelectorAll('.resume-section');

    // Drag start from skills list
    skillsList.addEventListener('dragstart', (e) => {
      if (e.target.tagName === 'DIV') {
        e.dataTransfer.setData('text/plain', e.target.textContent);
      }
    });

    // Allow drop into resume sections
    sections.forEach((section) => {
      section.addEventListener('dragover', (e) => e.preventDefault());
      section.addEventListener('drop', (e) => {
        e.preventDefault();
        const text = e.dataTransfer.getData('text/plain');
        const newItem = document.createElement('div');
        newItem.textContent = text;
        section.appendChild(newItem);
      });
    });

    // Add custom skills to the left column
    function addCustomSkills() {
      const inputs = document.querySelectorAll('.custom-inputs input');
      inputs.forEach((input) => {
        const value = input.value.trim();
        if (value !== '') {
          const newSkill = document.createElement('div');
          newSkill.textContent = value;
          newSkill.setAttribute('draggable', 'true');
          skillsList.appendChild(newSkill);
          input.value = '';
        }
      });
    }

    // PDF Download
    function downloadPDF() {
      const element = document.getElementById('exportArea');

      // Defensive: verify library loaded
      if (typeof html2pdf === 'undefined') {
        alert('PDF generator is not available. Please check your network and try again.');
        console.error('[PDF] html2pdf.js not loaded. Check the CDN/script tag.');
        return;
      }

      // Sensible defaults
      const opt = {
        margin:       [10, 10, 10, 10],
        filename:     'resume.pdf',
        image:        { type: 'jpeg', quality: 0.98 },
        html2canvas:  {
          scale: Math.min(2, window.devicePixelRatio || 1.5),
          backgroundColor: '#ffffff',
          useCORS: true,
          allowTaint: false
        },
        jsPDF:        { unit: 'mm', format: 'a4', orientation: 'portrait' },
        pagebreak:    { mode: ['css', 'legacy'] }
      };

      html2pdf().from(element).set(opt).save();
    }
  </script>
</body>
</html>
