# Part D — GitHub Activities & Live Deployment Walkthrough

---

## Activity 1: Professional GitHub Account & Profile Setup

### Profile Metadata:
- **GitHub Username**: `suprithareddy060405`
- **GitHub Profile Link**: [https://github.com/suprithareddy060405](https://github.com/suprithareddy060405)
- **Bio**: Full Stack Developer | Learning Web Engineering, CSS Flexbox/Grid, Git & GitHub Workflows
- **Featured Repositories**:
  - `Day7-Assignment`: Introduction to Git & GitHub complete suite
  - `Day6-Assignment`: Responsive Web Design, Flexbox & CSS Grid

---

## Activity 2 & 3: Portfolio Project & GitHub Pages Live Deployment

### Portfolio Directory Location:
The Section 29/30 responsive portfolio project is stored at:
`github-activities/portfolio/` inside this repository.

### Live GitHub Pages Production URL:
🔗 **[https://suprithareddy060405.github.io/Day7-Assignment/](https://suprithareddy060405.github.io/Day7-Assignment/)**

### Step-by-Step GitHub Pages Deployment Setup:
1. Push repository code to `https://github.com/suprithareddy060405/Day7-Assignment`.
2. Navigate to Repository **Settings** tab → **Pages** (under Code and automation).
3. Under **Build and deployment**:
   - **Source**: Select `Deploy from a branch`.
   - **Branch**: Select `main` branch, directory `/ (root)`.
   - Click **Save**.
4. GitHub Actions automatically executes the deployment workflow (`pages-build-deployment`).
5. Live site becomes active at `https://suprithareddy060405.github.io/Day7-Assignment/`.

---

## Activity 4: Portfolio Update, Commit, Push & Live Re-verification

### Demonstrating Iterative Live Updates:

#### 1. Code Update Made:
Added a live GitHub Pages deployment badge to `github-activities/portfolio/index.html`:
```html
<span class="badge">🚀 Live GitHub Pages Deployment</span>
```

#### 2. Commit & Push Terminal Command:
```bash
git add github-activities/portfolio/index.html
git commit -m "docs(portfolio): update live deployment badge in hero section"
git push origin main
```

#### 3. Verification:
Navigated to `https://suprithareddy060405.github.io/Day7-Assignment/` to confirm live rendering of updated badge.

---

## Activity 5: Open Source Project Exploration (`facebook/react`)

### Selected Open Source Project:
- **Repository**: [facebook/react](https://github.com/facebook/react)
- **Stars**: ~230,000+ Stars
- **Primary Language**: JavaScript / TypeScript

### Inspection Findings & Analysis:

#### 1. Architecture Overview (from `README.md`):
React is an open-source JavaScript library for building user interfaces based on component architecture, declarative views, and a virtual DOM diffing engine.

#### 2. Repository Directory Structure Inspected:
- `packages/react`: Contains core React top-level APIs (`useState`, `useEffect`, `useContext`, `useMemo`).
- `packages/react-dom`: Contains DOM rendering algorithms (`createRoot`, `render`).
- `fixtures/`: Test harnesses and sample benchmark applications.
- `.github/workflows`: Extensive CI/CD pipelines executing unit tests across Node versions.

#### 3. Contribution Guidelines (`CONTRIBUTING.md`):
- All code contributions require signing a Contributor License Agreement (CLA).
- Code format enforced strictly via Prettier & ESLint.
- PRs must pass automated yarn tests (`yarn test`) before maintainers review code.
