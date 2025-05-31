# public
public/ — Static Files Accessible by the Browser
The public/ folder in a React app (especially one created using Create React App or Vite) contains static assets that are directly accessible via a URL.

Everything in public/ is served as-is without being bundled by Webpack or Vite.

✅ Common Contents of public/
File / Folder	Purpose
index.html	The main HTML template React mounts into (<div id="root"></div>)
favicon.ico	Browser tab icon
manifest.json	Used for Progressive Web Apps (optional)
robots.txt	Tells search engines how to crawl your site
logo.png or logo.svg	App or company logo
assets/	Folder for static images, PDFs, fonts, etc.
404.html	Custom 404 page for hosting (like GitHub Pages)

📌 Accessing Public Files in React
Files here are accessed using relative paths from the root:

jsx
Copy code
<img src="/assets/logo.png" alt="Logo" />
<a href="/assets/terms.pdf" target="_blank">Terms of Service</a>
⚠️ Don’t import files from public/ in your JavaScript. Use URLs like above.

🧠 When to Use public/ vs src/assets/
Use Case	Use public/	Use src/assets/
You want direct file access via URL	✅ Yes	❌ No
You want to import image in code	❌ No	✅ Yes (e.g., import img)
PDF downloads or SEO files	✅ Yes	❌ No
Images used in JSX or CSS	❌ (unless static path)	✅ Yes

🧾 Example Structure
plaintext
Copy code
public/
├── index.html
├── favicon.ico
├── logo.png
├── robots.txt
├── manifest.json
├── 404.html
└── assets/
    ├── js-course-cover.jpg
    ├── react-course-cover.jpg
    ├── terms.pdf
    └── privacy-policy.pdf
✨ Bonus: Inject Meta Tags in index.html
html
Copy code
<meta name="description" content="Learn coding with our online courses" />
<meta property="og:image" content="/assets/cover.jpg" />