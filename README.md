# Jefferson Arcanjo — Personal Website

My personal / portfolio website: an "about me" for recruiters and hiring managers,
covering my background, skills, experience, projects, education and contact details.

It's also a working demo of a small DevOps pipeline — a static site hosted on
**Amazon S3** and deployed automatically with **GitHub Actions** on every push to `main`.

## 🌐 Live site

**[jefferson-static-site-2025.s3-website-eu-west-1.amazonaws.com](http://jefferson-static-site-2025.s3-website-eu-west-1.amazonaws.com)**

## 🗂 Structure

```
aws-s3-static-site/
├── website/                 # Everything deployed to S3
│   ├── index.html           # Single-page site (About, Skills, Experience, Projects, Education, Contact)
│   ├── about.html           # Redirect → index.html#about (kept for old links)
│   ├── projects.html        # Redirect → index.html#projects
│   ├── contact.html         # Redirect → index.html#contact
│   ├── 404.html             # Error page
│   ├── robots.txt
│   ├── favicon.svg
│   ├── resume.pdf
│   ├── css/style.css        # Light + dark theme, no build step
│   └── js/main.js           # Theme toggle, mobile nav, scroll reveal
├── .github/workflows/deploy.yml
└── README.md
```

> Only the contents of `website/` are deployed to S3.

## 🛠 Built with

| Tech | Purpose |
|------|---------|
| HTML / CSS / vanilla JS | Site content, styling and behaviour (no framework, no build) |
| AWS S3 | Static website hosting |
| IAM | Least-privilege deploy user |
| AWS CLI | `s3 sync` in the pipeline |
| GitHub Actions | CI/CD — deploy on push to `main` |

## 🚀 Deployment

1. Push to `main`.
2. GitHub Actions loads AWS credentials from repository secrets
   (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`).
3. `aws s3 sync website/ s3://jefferson-static-site-2025 --delete` publishes the site.

## Working locally

It's plain static files — open `website/index.html` in a browser, or serve the folder:

```bash
python3 -m http.server --directory website 8000
```

## 👤 Author

**Jefferson Arcanjo** — BSc (Hons) Computing & IT, CCT College Dublin · AWS Certified Cloud Practitioner
GitHub: [Arcanjo-jefferson](https://github.com/Arcanjo-jefferson) ·
LinkedIn: [jeffersonarcanjo](https://www.linkedin.com/in/jeffersonarcanjo/)
