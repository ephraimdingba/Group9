HTML FILE OPENGR0UP  9

Task: Develop An App that allows users to generate and customize a digital business card

STEP BY STEP EXPLANATION
The HTML defines the layout and elements that appear on the webpage. It divides the page into two main sections — the control panel (left) and the card preview (right).

1🔹 a. Document Head
<head> ... </head>


Sets up metadata such as the page title and viewport settings.

Includes two external JavaScript libraries via CDN:

html2canvas: converts parts of the webpage (the card) into an image.

jsPDF: allows generating and downloading PDF files directly from the browser.

Contains internal <style> tags for CSS styling.

🔹 b. Page Layout
<div class="container"> ... </div>


This is the main wrapper that organizes the content into two columns:

Left side: input panel (user details, theme selection, buttons).

Right side: live card preview and short “How it works” section.

🔹 c. Control Panel

Inside the left column (<div class="panel">):

There are several <input> fields where users type:

Full name

Job title

Company

Email

Phone number

A theme section with color boxes (.theme-swatch) to choose the card’s accent color.

Two buttons:

Download PNG: saves the card as an image file.

Download PDF: saves it as a PDF file.

Each input has an id (e.g., id="name") that the JavaScript later uses to read the value and display it in the preview.

🔹 d. Card Preview Area

The right column contains:

A live preview card (<div class="biz-card">) divided into:

Left side: company name, personal info, and contact details.

Right side: accent color panel showing “Connect” and “Virtual Card.”

A “How it works” panel that briefly explains the user steps.

Each text element in the card (like the name, company, or email) also has an ID (previewName, previewCompany, etc.), allowing JavaScript to update them dynamically when the user types.

2. CSS SECTION (Design and Styling)

The CSS styles control the appearance, colors, and layout of the application.

🔹 a. CSS Variables
:root {
  --accent: #1e88e5;
  --bg: #ffffff;
  --text: #111827;
}


These define global color variables that can be changed dynamically through JavaScript when the user selects a theme.
It makes color updates smoother and consistent across the page.

🔹 b. Layout Styling

.container uses CSS Grid to make two responsive columns.

.panel styles the white boxes with rounded corners and shadow effects.

.field defines the spacing and look of each input box.

.theme-swatch creates the small clickable color boxes for theme selection.

🔹 c. Card Styling

.biz-card defines the card size, rounded edges, and shadow.

.left-side and .right-side handle the two main color blocks of the card.

.logo-dot creates the small colored square used as a decorative logo.

Font colors, sizes, and background gradients are applied for a professional look.

The design is also responsive, so on smaller screens (like phones), the two sections stack vertically.

3. JAVASCRIPT SECTION (Interactivity and Functionality)

The JavaScript makes the webpage interactive — handling live updates, theme changes, and file downloads.

🔹 a. Getting Elements
const inputName  = document.getElementById('name');
const previewName  = document.getElementById('previewName');


This retrieves the HTML elements by their id so JavaScript can read or modify their content.
It does this for all form fields and their corresponding preview text areas.

🔹 b. Live Preview Function
function updatePreview() {
  previewName.textContent = inputName.value || 'Full Name';
}


Reads the text from each input field.

Updates the preview card’s text instantly.

Uses the input event listener to detect when the user types, so the card updates live without refreshing.

🔹 c. Theme Selection
themes.addEventListener('click', (e) => { ... });


Detects when a color swatch is clicked.

Reads its color values stored in data-accent, data-bg, and data-text.

Calls applyTheme() to update the global CSS variables, which instantly change the card’s color scheme.

🔹 d. Download as PNG
html2canvas(bizCard, opts)


The html2canvas library takes a “screenshot” of the .biz-card section.

Converts it into an image (canvas object).

Automatically triggers a download using a hidden <a> link.

🔹 e. Download as PDF
const pdf = new jsPDF({ unit: 'mm', format: 'a4' });
pdf.addImage(imgData, 'PNG', x, y, drawW, drawH);
pdf.save(${name}_card.pdf);


Uses jsPDF to create a new A4-sized PDF document.

Adds the previously captured card image (imgData) into the PDF page.

Centers and scales the image proportionally.

Prompts the user to download the generated PDF file.

🔹 f. Initialization
(function initTheme() { ... })();


This runs once when the page loads to apply the default selected theme and ensure the card preview starts with correct colors.

4. Overall Workflow

The user opens the page.

The script sets default values and loads the default theme.

The user types their details — the preview updates live.

The user selects a theme — the card’s color updates instantly.

The user clicks “Download PNG” or “Download PDF” — the card is saved as an image or PDF.

Everything happens client-side (in the browser). No internet uploads or backend server are required.

Summary
Component	Role
HTML	Defines the structure and content of the interface (inputs, preview card, buttons).
CSS	Controls visual design, layout, colors, fonts, and responsiveness.
JavaScript	Adds live interactivity, theme switching, and file download features.
html2canvas	Captures the card as an image directly from the screen.
jsPDF
 TO EDIT
