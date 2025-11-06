# Technology Stack

  

## Frontend Framework

- **Static HTML/CSS/JavaScript** - No build process required

- **Tailwind CSS 2.2.19** - Utility-first CSS framework via CDN

- **Font Awesome 6.0.0** - Icon library via CDN

- **Inter Font** - Primary typography from Google Fonts

  

## Deployment

- **AWS Amplify** - Static site hosting and deployment

- **No build commands** - Direct file serving from repository

- **Custom headers** - Cache-Control: no-store for all files

- **URL rewrites** - Clean URLs without .html extensions

  

## Browser Support

- **Tailwind Browser 4** - Modern CSS features

- **Responsive design** - Mobile-first approach with breakpoints

- **Progressive enhancement** - Works without JavaScript

  

## Development Workflow

```bash

# No build process - direct file editing

# Preview locally with any static server:

python -m http.server 8000

# or

npx serve .

  

# Deploy via git push to main branch (Amplify auto-deploys)

```

