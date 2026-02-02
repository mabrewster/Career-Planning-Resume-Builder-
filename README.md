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
      /* Make sure content can grow and be fully captured */
      overflow: visible;
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

    /* Optional: nicer output when rendering to PDF (applies only during capture) */
    .for-pdf, .for-pdf * {
      box-shadow: none !important;
    }
    .for-pdf .resume-section {
      border-color: #e6e6e6 !important; /* softer border in PDF */
    }
  </style>

  <!-- Bundle includes html2canvas + jsPDF -->
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
        if (!text) return;
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
<script>
  async function downloadPDF() {
    const exportEl = document.getElementById('exportArea');

    // Verify libraries from the html2pdf bundle
    const hasH2C = typeof window.html2canvas !== 'undefined';
    const hasJsPDF = window.jspdf && window.jspdf.jsPDF;
    if (!hasH2C || !hasJsPDF) {
      alert('PDF generator is not available. Please reload and try again.');
      console.error('Missing libs:', { html2canvas: hasH2C, jsPDF: !!hasJsPDF });
      return;
    }

    // Wait for images (if any) to finish loading inside the resume
    const waitForImages = (root) => {
      const imgs = Array.from(root.querySelectorAll('img'));
      if (imgs.length === 0) return Promise.resolve();
      return Promise.all(
        imgs.map(img => img.complete ? Promise.resolve() :
          new Promise(res => { img.onload = img.onerror = res; })
        )
      );
    };

    exportEl.classList.add('for-pdf');
    await waitForImages(exportEl);
    // Let the browser paint any last DOM updates before capture
    await new Promise(requestAnimationFrame);

    try {
      const scale = Math.min(2, window.devicePixelRatio || 1.5);
      const canvas = await window.html2canvas(exportEl, {
        scale,
        backgroundColor: '#ffffff',
        useCORS: true,
        allowTaint: false,
        logging: false
      });

      const imgData = canvas.toDataURL('image/jpeg', 0.98);
      const { jsPDF } = window.jspdf;
      const pdf = new jsPDF('p', 'mm', 'a4');

      const pageWidth = pdf.internal.pageSize.getWidth();   // ~210mm
      const pageHeight = pdf.internal.pageSize.getHeight(); // ~297mm
      const margin = 10;                                    // mm margins
      const usableWidth = pageWidth - margin * 2;

      // Canvas sizes in px
      const imgWidthPx = canvas.width;
      const imgHeightPx = canvas.height;

      // Pixels per mm (fit to width)
      const pxPerMm = imgWidthPx / usableWidth;

      // Usable page height in px (convert mm → px)
      const pageUsableHeightPx = Math.floor((pageHeight - margin * 2) * pxPerMm);

      // 🔁 Slice big canvas into pages
      let sY = 0;
      let pageIndex = 0;

      while (sY < imgHeightPx) {
        const sliceHeightPx = Math.min(pageUsableHeightPx, imgHeightPx - sY);

        const pageCanvas = document.createElement('canvas');
        pageCanvas.width = imgWidthPx;
        pageCanvas.height = sliceHeightPx;

        const ctx = pageCanvas.getContext('2d');
        // Improve slice quality
        ctx.imageSmoothingEnabled = true;
        ctx.imageSmoothingQuality = 'high';

        // Draw slice from main canvas → page canvas
        ctx.drawImage(
          canvas,
          0, sY, imgWidthPx, sliceHeightPx, // source rect
          0, 0, imgWidthPx, sliceHeightPx   // dest rect
        );

        const pageImgData = pageCanvas.toDataURL('image/jpeg', 0.98);
        const sliceHeightMm = sliceHeightPx / pxPerMm;

        if (pageIndex > 0) pdf.addPage();
        pdf.addImage(pageImgData, 'JPEG', margin, margin, usableWidth, sliceHeightMm);

        sY += sliceHeightPx;
        pageIndex++;
      }

      pdf.save('resume.pdf');
    } catch (err) {
      console.error('PDF generation failed:', err);
      alert('Sorry, the PDF could not be generated. Try reloading the page or another browser.');
    } finally {
      exportEl.classList.remove('for-pdf');
    }
  }
</script>
