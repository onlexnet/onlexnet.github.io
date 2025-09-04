# OnLex Website - Hugo Static Site

OnLex Website is a Polish business website built with Hugo static site generator using the Ananke theme. The site features company information pages (About, Services, Contact) and is deployed via GitHub Actions to GitHub Pages.

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Working Effectively

### Initial Setup and Dependencies
- Install Hugo v0.128.0 or newer (REQUIRED - apt version 0.123.7 is incompatible with theme):
  - `cd /tmp`
  - `wget https://github.com/gohugoio/hugo/releases/download/v0.137.1/hugo_extended_0.137.1_linux-amd64.tar.gz`
  - `tar -xzf hugo_extended_0.137.1_linux-amd64.tar.gz`
  - `sudo cp hugo /usr/local/bin/hugo`
  - `export PATH="/usr/local/bin:$PATH"`
  - `hugo version` (should show v0.137.1 or newer)

### Bootstrap and Build Process
- Initialize theme submodule (REQUIRED for first clone):
  - `git submodule init`
  - `git submodule update` -- takes ~30 seconds. NEVER CANCEL.
- Build the site:
  - `hugo` -- takes ~100ms. Fast build.
  - `hugo --buildDrafts` -- includes draft content, takes ~100ms
  - `hugo --minify` -- production build with minification, takes ~100ms

### Development Server
- Run development server:
  - `hugo server --bind 0.0.0.0 --port 1313`
  - Server starts in ~2 seconds
  - Access at `http://localhost:1313`
  - Supports live reload for file changes
  - Press Ctrl+C to stop

### Build Timing and Expectations
- **Hugo build**: ~100ms (extremely fast)
- **Theme download**: ~30 seconds for first time
- **Development server startup**: ~2 seconds
- **Git submodule update**: ~30 seconds
- All builds are fast - NO special timeout considerations needed

## Validation

### Always Test These Scenarios After Changes
1. **Theme and Build Validation**:
   - Verify theme submodule: `ls -la themes/ananke/` (should contain theme files, not empty)
   - Build without errors: `hugo --buildDrafts`
   - Check generated files: `ls -la public/` (should contain HTML files)

2. **Development Server Validation**:
   - Start server: `hugo server --bind 0.0.0.0 --port 1313`
   - Navigate to `http://localhost:1313`
   - Test navigation: Home → O nas (About) → Usługi (Services) → Kontakt (Contact)
   - Verify all pages load correctly with Polish content

3. **Production Build Validation**:
   - Clean build: `rm -rf public/`
   - Production build: `hugo --minify`
   - Verify output directory: `ls -la public/`

### Manual Testing Requirements
- ALWAYS test the full website navigation after making content changes
- Verify Polish language content displays correctly
- Test all menu links work (Home, O nas, Usługi, Kontakt)
- Ensure responsive design works on different screen sizes

## Project Structure

### Key Directories and Files
```
.
├── .github/workflows/hugo.yml    # GitHub Actions deployment
├── .devcontainer/                # VS Code dev container config
├── content/                      # Site content (Markdown)
│   ├── _index.md                # Homepage
│   ├── about.md                 # About page (O nas)
│   ├── services.md              # Services page (Usługi)
│   └── contact.md               # Contact page (Kontakt)
├── themes/ananke/               # Hugo theme (git submodule)
├── hugo.yaml                    # Hugo configuration
├── public/                      # Generated site (excluded from git)
└── resources/                   # Hugo resources cache (excluded from git)
```

### Content Management
- All content files are in `content/` directory
- Content uses Hugo front matter format with TOML (+++...+++)
- All content is currently marked as `draft = true`
- Site language is set to Polish (`languageCode: 'pl-pl'`)
- Site title: "OnLex - Nazwa Twojej Firmy"

### Theme Information
- Uses Ananke theme as git submodule
- Theme location: `themes/ananke/`
- Theme repository: https://github.com/theNewDynamic/gohugo-theme-ananke
- Requires Hugo v0.128.0+ (critical compatibility requirement)

## Deployment

### GitHub Actions Workflow
- File: `.github/workflows/hugo.yml`
- Triggers: Push to main branch, manual dispatch
- Deploys to GitHub Pages automatically
- Uses Hugo extended version for Sass/SCSS support
- Build command: `hugo --minify --baseURL "${{ steps.pages.outputs.base_url }}/"`

### Local Production Testing
- Build for production: `hugo --minify`
- Output directory: `public/`
- Static files ready for any web server

## Common Commands Reference

### Development Workflow
- `git submodule update --remote` -- update theme to latest version
- `hugo new content/posts/my-post.md` -- create new content
- `hugo server -D` -- run server with drafts
- `hugo --buildDrafts --minify` -- build with drafts and minification

### Content Management
- Content files use TOML front matter (+++...+++)
- Remove `draft = true` to publish content
- Date format: `date = '2025-09-04T20:23:18Z'`

### Environment Information
- Hugo version: v0.137.1+ required
- Build environment: Linux/amd64
- Go modules support enabled
- Extended Hugo features available (Sass/SCSS, WebP)

## Important Notes

### Critical Requirements
- **NEVER use apt-get Hugo** - version 0.123.7 is incompatible with theme
- **ALWAYS download Hugo v0.137.1+** from GitHub releases
- **ALWAYS run `git submodule init && git submodule update`** on fresh clone
- **ALWAYS use `--buildDrafts`** flag to include all current content (marked as drafts)

### File Exclusions
- `public/` and `resources/_gen/` are build artifacts - excluded from git
- `.hugo_build.lock` is a build lock file - excluded from git
- Use `.gitignore` to prevent committing build artifacts

### Troubleshooting
- If theme missing: Run `git submodule init && git submodule update`
- If build fails with Sass errors: Ensure Hugo extended version is installed
- If old Hugo version: Download latest from GitHub releases, don't use apt
- If pages don't show: Add `--buildDrafts` flag to include draft content

## Common Outputs for Reference

### Repository Root Contents
```
.devcontainer  .git  .github  .gitmodules  .hugo_build.lock  archetypes  content  hugo.yaml  public  resources  themes
```

### Hugo Version Output
```
hugo v0.137.1-17e15b2148cee6da923acd7adf2ec31ea6b3415c+extended linux/amd64 BuildDate=2024-11-05T11:49:09Z VendorInfo=gohugoio
```

### Successful Build Output
```
Start building sites … 
                   | EN  
-------------------+-----
  Pages            | 11  
  Paginator pages  |  0  
  Non-page files   |  0  
  Static files     |  1  
  Processed images |  0  
  Aliases          |  0  
  Cleaned          |  0  

Total in 78 ms
```