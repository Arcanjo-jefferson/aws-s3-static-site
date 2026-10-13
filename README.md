# Jefferson Arcanjo — Personal Website

My personal / portfolio website: an "about me" for recruiters and hiring managers,
covering my background, skills, experience, projects, education and contact details.

It's also a working demo of a small DevOps pipeline: static files stored in
**Amazon S3**, served over **HTTPS through Amazon CloudFront**, and uploaded to S3
automatically with **GitHub Actions** on every push to `main`.

## 🌐 Live site

**[d1sahnszekrzm.cloudfront.net](https://d1sahnszekrzm.cloudfront.net)**

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
| AWS S3 | Stores the website files |
| Amazon CloudFront | Delivers the website over HTTPS and caches content |
| IAM | Least-privilege deploy user |
| AWS CLI | `s3 sync` in the pipeline |
| GitHub Actions | CI/CD — deploy on push to `main` |

## 🚀 Deployment

1. Push to `main`.
2. GitHub Actions loads AWS credentials from repository secrets
   (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`).
3. The workflow uploads the website files with:

   ```bash
   aws s3 sync website/ s3://jefferson-static-site-2025 --delete --exclude ".DS_Store" --exclude ".git*"
   ```

4. CloudFront serves the files at the HTTPS address above. The current workflow
   does not invalidate CloudFront's cache, so visitors may see a previous version
   until cached files expire. To make an update visible promptly, create an
   invalidation for `/*` in the CloudFront console after the S3 upload succeeds.

## HTTPS hosting configuration

- S3 bucket: `jefferson-static-site-2025` (Ireland, `eu-west-1`).
- CloudFront distribution: `EAIS9UMZXD9S8`.
- CloudFront domain: `d1sahnszekrzm.cloudfront.net`.
- Default root object: `index.html`.
- Viewer protocol policy: **Redirect HTTP to HTTPS**.
- Origin: the regular S3 bucket endpoint, with **Origin Access Control (OAC)**
  configured to sign requests.

The bucket policy must allow this CloudFront distribution to read the objects.
Once CloudFront access is verified, remove the public-read policy statement and
turn on S3 Block Public Access. This restricts website reads to CloudFront while
allowing the authorised GitHub Actions deployment user to continue uploading files.

The old S3 website endpoint supports HTTP only. Use the CloudFront HTTPS address
for shared links.

## Working locally

It's plain static files — open `website/index.html` in a browser, or serve the folder:

```bash
python3 -m http.server --directory website 8000
```

## 👤 Author

**Jefferson Arcanjo** — BSc (Hons) Computing & IT, CCT College Dublin · AWS Certified Cloud Practitioner
GitHub: [Arcanjo-jefferson](https://github.com/Arcanjo-jefferson) ·
LinkedIn: [jeffersonarcanjo](https://www.linkedin.com/in/jeffersonarcanjo/)
