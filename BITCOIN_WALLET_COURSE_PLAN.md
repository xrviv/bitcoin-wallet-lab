# Bitcoin Wallet Android App Course — Complete Project Plan

## Executive Summary

This plan covers three major objectives:
1. **Repository Organization** — File structure, naming conventions, branching strategy
2. **Update Schedule** — Maintenance cadence, content review cycles, version management
3. **GitHub Pages Publishing** — Documentation site setup, deployment workflow

**Timeline Overview:**
- Phase 1 (Days 1-3): Repository setup and initial structure
- Phase 2 (Days 4-7): Content population and GitHub Pages configuration
- Phase 3 (Ongoing): Maintenance and update cycles

---

## Part 1: Repository Organization

### 1.1 Root Directory Structure

```
bitcoin-wallet-android-course/
│
├── README.md                    # Project overview, prerequisites, quick start
├── COURSE_OUTLINE.md            # Full 11-week curriculum
├── CONTRIBUTING.md              # How to contribute/report issues
├── LICENSE                      # MIT or Apache 2.0 recommended
├── .gitignore                   # Android/Kotlin/Gradle ignores
├── CODE_OF_CONDUCT.md           # Community guidelines
├── CHANGELOG.md                 # Version history
│
├── docs/                        # Course content (GitHub Pages source)
│   ├── index.md                 # Landing page
│   ├── _config.yml              # Jekyll configuration
│   ├── part-1-foundation/
│   ├── part-2-android-core/
│   ├── part-3-cryptography/
│   ├── part-4-bitcoin-core/
│   ├── part-5-security/
│   ├── part-6-reproducible-builds/
│   ├── part-7-final-app/
│   └── assets/
│       ├── images/
│       ├── diagrams/
│       └── css/
│
├── code/                        # Progressive app development
│   ├── starter/                 # Blank project template
│   ├── part-1-foundation/       # Code state after Part 1
│   ├── part-2-android-core/     # Code state after Part 2
│   ├── part-3-cryptography/     # Code state after Part 3
│   ├── part-4-bitcoin-core/     # Code state after Part 4
│   ├── part-5-security/         # Code state after Part 5
│   ├── part-6-reproducible/     # Code state after Part 6
│   └── final/                   # Complete application
│
├── exercises/                   # Practice problems
│   ├── part-1/
│   │   ├── exercise-1-variables/
│   │   ├── exercise-2-functions/
│   │   └── exercise-3-kotlin-basics/
│   ├── part-2/
│   ├── part-3/
│   ├── part-4/
│   ├── part-5/
│   └── part-6/
│
├── solutions/                   # Exercise answers (separate for self-pacing)
│   ├── part-1/
│   ├── part-2/
│   ├── part-3/
│   ├── part-4/
│   ├── part-5/
│   └── part-6/
│
├── resources/                   # Reference materials
│   ├── cheatsheets/
│   │   ├── kotlin-cheatsheet.md
│   │   ├── android-cheatsheet.md
│   │   ├── bitcoin-cheatsheet.md
│   │   └── git-cheatsheet.md
│   ├── glossary.md
│   └── external-links.md
│
└── .github/                     # GitHub-specific config
    ├── workflows/
    │   ├── build-android.yml    # CI for Android code
    │   ├── deploy-pages.yml     # GitHub Pages deployment
    │   └── lint-docs.yml        # Markdown linting
    ├── ISSUE_TEMPLATE/
    │   ├── bug_report.md
    │   ├── question.md
    │   └── content_request.md
    └── PULL_REQUEST_TEMPLATE.md
```

### 1.2 Documentation Structure (docs/)

Each part folder follows this pattern:

```
docs/part-X-topic/
├── index.md                     # Part overview and learning objectives
├── week-N-topic/
│   ├── lesson-1-subtopic.md
│   ├── lesson-2-subtopic.md
│   └── quiz.md                  # Self-assessment questions
├── summary.md                   # Part recap and key takeaways
└── next-steps.md                # Transition to next part
```

**Detailed Example — Part 3 Cryptography:**

```
docs/part-3-cryptography/
├── index.md
├── week-5-fundamentals/
│   ├── lesson-1-hash-functions.md
│   ├── lesson-2-public-private-keys.md
│   ├── lesson-3-digital-signatures.md
│   └── quiz.md
├── week-6-bitcoin-crypto/
│   ├── lesson-1-ecdsa-secp256k1.md
│   ├── lesson-2-bip32-hd-wallets.md
│   ├── lesson-3-bip39-mnemonics.md
│   └── quiz.md
├── summary.md
└── next-steps.md
```

### 1.3 Code Organization (code/)

Each code folder is a **complete, buildable Android project** representing the state after completing that part:

```
code/part-4-bitcoin-core/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/bitcoinwallet/
│   │   │   │   ├── MainActivity.kt
│   │   │   │   ├── data/
│   │   │   │   ├── domain/
│   │   │   │   ├── presentation/
│   │   │   │   └── crypto/
│   │   │   ├── res/
│   │   │   └── AndroidManifest.xml
│   │   └── test/
│   └── build.gradle.kts
├── build.gradle.kts
├── settings.gradle.kts
├── gradle.properties
└── README.md                    # What was added in this part
```

### 1.4 Branching Strategy

```
main                             # Stable, reviewed content only
├── develop                      # Integration branch for new content
│   ├── feature/part-1-content   # New lesson development
│   ├── feature/part-2-exercises # Exercise development
│   ├── fix/typo-correction      # Quick fixes
│   └── update/dependencies      # Gradle/library updates
└── gh-pages                     # Auto-deployed from docs/
```

**Branch Rules:**
- `main` requires PR review before merge
- `develop` is the working branch for content creators
- Feature branches are deleted after merge
- `gh-pages` is auto-managed by GitHub Actions

### 1.5 Naming Conventions

| Element | Convention | Example |
|---------|------------|---------|
| Folders | lowercase-kebab-case | `part-3-cryptography/` |
| Markdown files | lowercase-kebab-case | `lesson-2-bip32-hd-wallets.md` |
| Kotlin files | PascalCase | `WalletViewModel.kt` |
| Images | lowercase-kebab-descriptive | `ecdsa-signing-flow.png` |
| Branches | type/short-description | `feature/part-5-security` |
| Commits | Conventional Commits | `feat(part-3): add BIP39 lesson` |

### 1.6 Commit Message Format

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

**Types:**
- `feat`: New content or feature
- `fix`: Bug fixes or corrections
- `docs`: Documentation changes
- `style`: Formatting, no code change
- `refactor`: Code restructuring
- `test`: Adding tests
- `chore`: Maintenance tasks

**Examples:**
```
feat(part-3): add ECDSA explanation with diagrams
fix(part-2): correct Room database migration code
docs(readme): update prerequisites section
chore(deps): bump Kotlin to 1.9.22
```

---

## Part 2: Update Schedule

### 2.1 Content Update Cadence

| Cycle | Frequency | Focus | Owner |
|-------|-----------|-------|-------|
| **Hot Fixes** | As needed | Typos, broken links, critical errors | Any contributor |
| **Minor Updates** | Monthly | Code updates, clarifications, FAQ additions | Maintainer |
| **Major Reviews** | Quarterly | Dependency updates, new Android versions, Bitcoin protocol changes | Core team |
| **Full Audit** | Annually | Complete curriculum review, relevance check | Course lead |

### 2.2 Detailed Timetable

#### Year 1 Schedule

| Month | Week | Activity | Deliverables |
|-------|------|----------|--------------|
| **Month 1** | 1-2 | Repository setup, structure creation | Initial commit, folder structure |
| | 3-4 | Part 1 content (Foundation) | Lessons, exercises, code |
| **Month 2** | 1-2 | Part 2 content (Android Core) | Lessons, exercises, code |
| | 3-4 | Part 3 content (Cryptography) | Lessons, exercises, code |
| **Month 3** | 1-2 | Part 4 content (Bitcoin Core) | Lessons, exercises, code |
| | 3-4 | Part 5 content (Security) | Lessons, exercises, code |
| **Month 4** | 1-2 | Part 6-7 content (Builds, Final App) | Lessons, exercises, code |
| | 3-4 | **First quarterly review** | Bug fixes, feedback integration |
| **Month 5** | 1-2 | GitHub Pages refinement | CSS, navigation, search |
| | 3 | Beta testing with users | Collect feedback |
| | 4 | Address beta feedback | Revisions |
| **Month 6** | 1-2 | Official launch | Announcement, promotion |
| | 3-4 | Post-launch monitoring | Issue triage, quick fixes |
| **Month 7-9** | - | Monthly maintenance cycle | Updates per 2.1 cadence |
| **Month 10** | - | **Second quarterly review** | Android updates, library bumps |
| **Month 12** | - | **Annual audit** | Full curriculum review |

### 2.3 Dependency Update Schedule

| Dependency | Check Frequency | Update Trigger |
|------------|-----------------|----------------|
| Android Gradle Plugin | Monthly | Security patches, new features |
| Kotlin | Monthly | Minor versions within 2 weeks |
| AndroidX libraries | Monthly | Security patches immediately |
| Bitcoin libraries (bitcoinj, etc.) | Bi-weekly | Any protocol-relevant changes |
| Jekyll/GitHub Pages gems | Quarterly | Breaking changes only |

### 2.4 Review Checklist Templates

**Monthly Review Checklist:**
```markdown
## Monthly Review — [Month Year]

### Code Verification
- [ ] All code samples compile without errors
- [ ] Unit tests pass
- [ ] Tested on latest Android emulator

### Content Check
- [ ] External links verified
- [ ] Screenshots match current UI
- [ ] No reported typos/issues pending

### Dependencies
- [ ] Gradle dependencies scanned for vulnerabilities
- [ ] Any critical updates applied

### Community
- [ ] Open issues triaged
- [ ] PRs reviewed and merged
```

**Quarterly Review Checklist:**
```markdown
## Quarterly Review — Q[N] [Year]

### Major Updates
- [ ] Android SDK version compatibility
- [ ] Kotlin version alignment
- [ ] Bitcoin protocol changes reviewed
- [ ] New best practices incorporated

### Curriculum Relevance
- [ ] Market demand assessment
- [ ] Competitor course analysis
- [ ] Student feedback synthesis

### Infrastructure
- [ ] CI/CD pipelines functional
- [ ] GitHub Pages deployment verified
- [ ] Repository health (stale branches, etc.)
```

---

## Part 3: GitHub Pages Publishing

### 3.1 Technology Stack

- **Static Site Generator:** Jekyll (native GitHub Pages support)
- **Theme:** `just-the-docs` (excellent for documentation)
- **Hosting:** GitHub Pages (free)
- **Domain:** `<username>.github.io/bitcoin-wallet-android-course`

### 3.2 Configuration Files

**`docs/_config.yml`:**
```yaml
title: Bitcoin Wallet Android Course
description: Build a Bitcoin wallet from scratch with Android and Kotlin
theme: just-the-docs
url: "https://<username>.github.io"
baseurl: "/bitcoin-wallet-android-course"

# Navigation structure
nav_order: 1

# Enable search
search_enabled: true
search.heading_level: 3

# Aux links (top right)
aux_links:
  "GitHub Repo":
    - "https://github.com/<username>/bitcoin-wallet-android-course"

# Footer
footer_content: "Copyright &copy; 2025. Distributed under MIT License."

# Collections for parts
collections:
  part-1-foundation:
    output: true
    permalink: /:collection/:name
  part-2-android-core:
    output: true
    permalink: /:collection/:name
  # ... continue for all parts

# Code highlighting
highlighter: rouge
markdown: kramdown
kramdown:
  syntax_highlighter: rouge
  syntax_highlighter_opts:
    block:
      line_numbers: true

# Plugins
plugins:
  - jekyll-seo-tag
  - jekyll-sitemap
```

### 3.3 GitHub Actions Deployment

**`.github/workflows/deploy-pages.yml`:**
```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
    paths:
      - 'docs/**'
      - '.github/workflows/deploy-pages.yml'
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.2'
          bundler-cache: true
          working-directory: docs

      - name: Setup Pages
        uses: actions/configure-pages@v4

      - name: Build with Jekyll
        run: |
          cd docs
          bundle install
          bundle exec jekyll build --baseurl "${{ steps.pages.outputs.base_path }}"
        env:
          JEKYLL_ENV: production

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: docs/_site

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### 3.4 Page Structure

**Landing Page (`docs/index.md`):**
```markdown
---
layout: home
title: Home
nav_order: 1
---

# Bitcoin Wallet Android Course

Build a fully functional Bitcoin wallet for Android, from zero to deployment.

## What You'll Learn

- Android development with Kotlin
- Bitcoin cryptography (BIP32, BIP39, ECDSA)
- Secure key storage and biometric authentication
- Reproducible builds for trust verification

## Prerequisites

- Basic programming knowledge
- Computer with 8GB+ RAM
- ~20GB free disk space

[Get Started →](part-1-foundation/){: .btn .btn-primary }
[View on GitHub](https://github.com/<username>/bitcoin-wallet-android-course){: .btn }
```

### 3.5 Enabling GitHub Pages

**Manual Steps (one-time setup):**

1. Go to repository **Settings** → **Pages**
2. Under **Source**, select **GitHub Actions**
3. First push to `main` with `docs/` folder triggers deployment
4. Site available at `https://<username>.github.io/bitcoin-wallet-android-course`

### 3.6 Custom Domain (Optional)

If you own a domain:

1. Create `docs/CNAME` with your domain:
   ```
   learn.yourdomain.com
   ```
2. Configure DNS:
   - CNAME record: `learn` → `<username>.github.io`
3. Enable HTTPS in repository Settings → Pages

---

## Part 4: Implementation Timetable

### Phase 1: Repository Setup (Days 1-3)

| Day | Task | Commands/Actions |
|-----|------|------------------|
| **1** | Create GitHub repository | GitHub web UI |
| | Clone locally | `git clone <repo-url>` |
| | Create folder structure | `mkdir -p docs code exercises solutions resources .github/workflows` |
| | Add .gitignore | Android + Jekyll ignores |
| | Initial commit | `git add . && git commit -m "chore: initial repository structure"` |
| **2** | Create README.md | Project overview |
| | Create COURSE_OUTLINE.md | Full curriculum |
| | Create CONTRIBUTING.md | Contribution guidelines |
| | Create LICENSE | MIT license |
| | Commit | `git commit -m "docs: add root documentation files"` |
| **3** | Setup docs/_config.yml | Jekyll configuration |
| | Create docs/index.md | Landing page |
| | Create docs/Gemfile | Jekyll dependencies |
| | Setup GitHub Actions | deploy-pages.yml |
| | Push and verify | `git push origin main` |
| | Enable GitHub Pages | Repository Settings |

### Phase 2: Content Population (Days 4-14)

| Day | Task | Deliverables |
|-----|------|--------------|
| **4-5** | Part 1 documentation | docs/part-1-foundation/* |
| **6-7** | Part 1 code + exercises | code/part-1/, exercises/part-1/ |
| **8-9** | Part 2 documentation | docs/part-2-android-core/* |
| **10-11** | Part 2 code + exercises | code/part-2/, exercises/part-2/ |
| **12** | Parts 3-4 documentation | docs/part-3-*, docs/part-4-* |
| **13** | Parts 5-7 documentation | docs/part-5-*, docs/part-6-*, docs/part-7-* |
| **14** | Final review and launch | Full test, announcement |

### Phase 3: Ongoing Maintenance

```
Week 1 of each month:
├── Monday: Dependency scan
├── Tuesday: Issue triage
├── Wednesday: Content updates
├── Thursday: Code verification
└── Friday: Deploy and verify

Quarter end:
├── Full curriculum review
├── Android version compatibility check
├── Bitcoin protocol updates review
└── Community feedback synthesis

Year end:
├── Complete audit
├── Roadmap planning
└── Major version release
```

---

## Part 5: Quick Start Commands

### Initial Setup

```bash
# 1. Create repository on GitHub (web UI), then:
git clone https://github.com/<username>/bitcoin-wallet-android-course.git
cd bitcoin-wallet-android-course

# 2. Create structure
mkdir -p docs/{part-1-foundation,part-2-android-core,part-3-cryptography,part-4-bitcoin-core,part-5-security,part-6-reproducible-builds,part-7-final-app,assets/{images,diagrams,css}}
mkdir -p code/{starter,part-1-foundation,part-2-android-core,part-3-cryptography,part-4-bitcoin-core,part-5-security,part-6-reproducible,final}
mkdir -p exercises/{part-1,part-2,part-3,part-4,part-5,part-6}
mkdir -p solutions/{part-1,part-2,part-3,part-4,part-5,part-6}
mkdir -p resources/cheatsheets
mkdir -p .github/{workflows,ISSUE_TEMPLATE}

# 3. Create placeholder files
touch docs/_config.yml docs/index.md docs/Gemfile
touch README.md COURSE_OUTLINE.md CONTRIBUTING.md LICENSE CHANGELOG.md CODE_OF_CONDUCT.md
touch .gitignore

# 4. Initial commit
git add .
git commit -m "chore: initial repository structure"
git push origin main
```

### Local Jekyll Preview

```bash
cd docs
bundle install
bundle exec jekyll serve
# Open http://localhost:4000/bitcoin-wallet-android-course
```

---

## Appendix A: File Templates

### README.md Template

```markdown
# Bitcoin Wallet Android Course

Learn to build a fully functional Bitcoin wallet for Android.

## 🎯 What You'll Build

A complete Bitcoin wallet with:
- HD wallet generation (BIP32/BIP39)
- Transaction creation and broadcasting
- Secure key storage with biometrics
- Reproducible builds

## 📋 Prerequisites

- Basic programming knowledge
- Computer: 8GB+ RAM, 20GB free space
- Time: ~11 weeks at 10-15 hours/week

## 🚀 Quick Start

1. [Start the course](https://username.github.io/bitcoin-wallet-android-course)
2. Clone this repo for code exercises
3. Follow along week by week

## 📁 Repository Structure

| Folder | Purpose |
|--------|---------|
| `docs/` | Course content (also powers the website) |
| `code/` | Progressive app code by section |
| `exercises/` | Practice problems |
| `solutions/` | Exercise answers |
| `resources/` | Cheatsheets and references |

## 📖 Course Outline

See [COURSE_OUTLINE.md](COURSE_OUTLINE.md) for the full curriculum.

## 🤝 Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## 📄 License

MIT License - see [LICENSE](LICENSE)
```

### .gitignore Template

```gitignore
# Android
*.iml
.gradle/
/local.properties
/.idea/
.DS_Store
/build/
/captures/
.externalNativeBuild/
.cxx/
*.apk
*.aab
*.ap_
*.dex

# Kotlin
*.class
*.log
*.jar

# Jekyll
docs/_site/
docs/.sass-cache/
docs/.jekyll-cache/
docs/.jekyll-metadata
docs/vendor/

# IDE
.vscode/
*.swp
*.swo

# OS
.DS_Store
Thumbs.db
```

---

## Appendix B: Success Metrics

Track these to measure course effectiveness:

| Metric | Target | Tool |
|--------|--------|------|
| GitHub Stars | 100 in 6 months | GitHub |
| Course Completions | Track via issues/discussions | GitHub |
| Page Views | 1000/month | GitHub Pages analytics |
| Open Issues | < 10 unresolved | GitHub |
| Time to First Response | < 48 hours | GitHub |
| Build Success Rate | 100% | GitHub Actions |

---

*Plan Version: 1.0*  
*Created: January 2025*  
*Next Review: April 2025*
