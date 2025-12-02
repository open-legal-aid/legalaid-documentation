# LegalAId - Community & Governance

## Mission & Values

### Mission
Demokratisierung von Rechtsberatung im Migrationsrecht für NGOs, RLCs und Beratungsstellen. **LegalAId macht Rechtswissen zugänglich, kostenlos und vertrauenswürdig.**

Democratization of legal advice in migration law for NGOs, RLCs, and advisory centers. LegalAId makes legal knowledge accessible, free, and trustworthy.


### Core Values

| Wert | Bedeutung |
|------|-----------|
| 🔓 **Offenheit** | Open Source, transparente Entscheidungen, Community-getrieben |
| 🛡️ **Vertrauen** | Kein Hype, klare Kommunikation der technischen Grenzen, qualitätsgeleitet |
| 🌍 **Gerechtigkeit** | Migrationsrecht muss allen zugänglich sein, nicht nur den Wohlhabenden/Privilegierten |
| 💪 **Empowerment** | Menschen (Berater:innen) sind im Mittelpunkt, nicht die Technologie |
| 🔒 **Privatsphäre** | Datenschutz by design, keine Cloud-Abhängigkeit |



Value	Meaning
🔓 **Openness**   Open source, transparent decision-making, community-driven
🛡️ **Trust**   No hype, clear communication of technical limitations, quality-focused
🌍 **Justice**   Migration law must be accessible to everyone, not just the wealthy/privileged
💪 **Empowerment**   People (advisors) are at the center, not technology
🔒 **Privacy**   Privacy by design, no cloud dependency

---

### Decision Making Process

```
Issue/Feature Request
    ↓
Discussion (GitHub Discussions / Discord)
    ↓
Core Team Consensus or Vote (if divergent views)
    ↓
Implementation
    ↓
Review + Merge
    ↓
Release & Announce
```

### Contributor Levels

| Level | Requirements | Privileges |
|-------|--------------|-----------|
| **User** | Uses LegalAId | Can report issues, request features |
| **Contributor** | 1+ merged PRs | Can review PRs, participate in discussions |
| **Maintainer** | 5+ significant contributions | Merge access, release authority |
| **Core Team** | Long-term commitment | Strategic decisions, version planning |

---

## How to Contribute

### Getting Started

1. **Fork the repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/legalaid.git
   cd legalaid
   ```

2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make changes**
   - Follow code style (see DEVELOPMENT.md)
   - Write tests for new features
   - Update documentation

4. **Submit PR**
   - Clear description of changes
   - Reference any related issues
   - Link to screenshots if UI changes

### Contribution Areas

#### Code

- **Frontend**: Vue.js components, accessibility, i18n
- **Backend**: FastAPI endpoints, RAG optimization, QA layers
- **DevOps**: Docker, CI/CD, deployment scripts
- **Testing**: Unit tests, integration tests, E2E tests

#### Documentation

- **User Guides**: How-tos for NGOs
- **API Docs**: Technical reference
- **Translation**: German ↔ English ↔ other languages
- **Examples**: Code samples, use-case walkthroughs

#### Community

- **Outreach**: Connect with NGOs, spread the word
- **User Support**: Help others in Discord/GitHub Discussions
- **Feedback**: User research, usability testing
- **Case Studies**: Document real-world implementations

#### 📋 Legal & Compliance

- **Legal Research**: Find & analyze migration law cases
- **Quality Assurance**: Verify answers against real jurisprudence
- **Privacy**: Ensure DSGVO compliance
- **Accessibility**: Test and improve WCAG 2.1 compliance

---

## Development Workflow

### Code Review Standards

**Good PRs**
- Clear description of why (not just what)
- Tests included
- Documentation updated
- Passes CI/CD checks
- 1-2 approvals before merge

**Reasons for rejection**
- No tests
- Documentation missing
- Breaks existing functionality
- Security concerns
- Inaccessible UI changes

### Testing Requirements

```python
# Backend tests
pytest tests/ --cov=backend

# Frontend tests
npm run test

# E2E tests
npm run test:e2e

# All must pass before merge
```

### Code Style

**Python (Backend)**
- Black formatting
- isort for imports
- Type hints on all functions
- Docstrings (Google style)

**JavaScript/Vue (Frontend)**
- Prettier formatting
- ESLint configuration
- TypeScript strict mode
- JSDoc comments

**Git Commits**
```
feat: Add new feature (emoji)
fix: Fix specific bug (emoji)
docs: Update documentation (emoji)
refactor: Code restructuring (emoji)
test: Add/update tests (emoji)

Examples:
feat: Add Whisper Arabic support
fix: Correct confidence scoring calculation
docs: Update deployment guide for Railway
```

---

## Communication Channels

### GitHub

- **Issues**: Bug reports, feature requests, roadmap tracking
- **Discussions**: General questions, design discussions
- **Projects**: Sprint planning, milestone tracking

### Discord (coming soon)

- **#general**: Announcements, general chat
- **#help**: User support
- **#dev**: Developer discussions
- **#legal**: Legal/compliance topics
- **#localization**: Translation efforts
- **#showcase**: User success stories

### Email

- **Contact**: tjiokdave@gmail.com
- **Team**: N.N.
- **For Urgent Issues**: N.N.

---

## Roadmap & Releases

### Version Strategy

```
X.Y.Z
├─ X = Major (breaking changes, new architecture)
├─ Y = Minor (new features, compatible)
└─ Z = Patch (bug fixes)

Example: 1.0.0 (MVP Release)
         1.1.0 (Add Familiennachzug Use-Case)
         1.1.1 (Fix confidence scoring bug)
```

### Release Schedule

- **MVP (6 months)**: 0.1.0 → 1.0.0
- **Post-MVP (Second Stage)**: 1.0.0 → 2.0.0
- **Quarterly minor releases**: 1.1.0, 1.2.0, 1.3.0, ...
- **Critical patches**: As needed

### Changelog Format

```markdown
## [1.0.0] - 2025-06-30
### Added
- Whisper.js multilingual audio input
- 5-Layer QA system implementation
- Advisor dashboard

### Changed
- Improved RAG confidence scoring
- Refactored session state machine

### Fixed
- IndexedDB persistence issue on mobile

### Security
- Added DSGVO-compliant session expiry
```

---

## Community Recognition

### Contributor Wall of Fame

We recognize all contributions on:
- **GitHub**: Contributors list
- **Website**: Community page
- **Quarterly Reports**: Feature spotlights

### Special Roles

**Legal Reviewers**
- Verify RAG answers against jurisprudence
- Monthly review of new legal sources
- Provide quality feedback

**NGO Champions**
- Advocate in their network
- Collect user feedback
- Help with localization

**Localization Leads**
- Translate UI/docs into new languages
- Cultural adaptation
- Community support in language

---

## Conflict Resolution

### Issue Resolution Process

1. **Respectful Discussion** (GitHub/Discord)
2. **Core Team Mediation** (if needed)
3. **Decision by Consensus** (preferred)
4. **Vote** (if consensus impossible)
5. **Final Appeal** (Project Lead)

### Code of Conduct Basics

**Do**
- Be respectful and inclusive
- Assume good intent
- Focus on ideas, not people
- Help others learn

**Don't**
- Discriminate or harass
- Be dismissive of concerns
- Spam or flood
- Share private information

---

## Sustainability & Funding

### Funding Model

| Source | Purpose | Timeline |
|--------|---------|----------|
| **Prototype Fund** | MVP Development | Months 1-6 |
| **Donations** | Community Support | Ongoing |
| **Grants** | Feature Development | Annual |
| **Sponsors** | Infrastructure | Ongoing |

### Donation Channels (coming soon)

- **Betterplace.org** (German-focused)
- **OpenCollective** (International)
- **Corporate Sponsors** (seeking legal & tech firms)

### Non-Profit Status (planned)

- **Verein**: LegalAId e.V. (association)
- **Gemeinnützigkeit**: Tax-exempt status
- **Board**: Diverse representation (NGO, tech, law)

---

## Long-Term Vision (Year 2+)

### Phase 2: Expansion

**Use-Cases (beyond Aufenthaltserlaubnis)**
- Familiennachzug (Family Reunification)
- Erstantrag (Initial Asylum Application)
- Beschwerdeverfahren (Appeal Process)

**Localization**
- Italian, Spanish, Portuguese
- Better multi-script support (Cyrillic, Greek)

**Integrations**
- Case management systems
- NGO databases
- Government info portals

### Phase 3: Network Building

**NGO Network**
- 100+ organizations using LegalAId
- Regular case law updates
- Collaborative legal research

**Research & Learning**
- Publishing case law analysis
- Policy recommendations to government
- Academic publications

**Sustainability**
- Self-funded through donations
- Government grants
- Foundation support

---

## Resources for Contributors

### Documentation

- **[DEVELOPMENT.md](./DEVELOPMENT.md)** - Setup & coding guidelines
- **[ARCHITECTURE.md](./ARCHITECTURE.md)** - Technical deep-dive
- **[DEPLOYMENT.md](./DEPLOYMENT.md)** - Infrastructure & ops
- **[API Docs](./backend/README.md)** - API reference

### External Resources

- **Vue.js 3**: https://vuejs.org/guide/
- **FastAPI**: https://fastapi.tiangolo.com/
- **LlamaIndex**: https://docs.llamaindex.ai/
- **WCAG 2.1**: https://www.w3.org/WAI/WCAG21/quickref/

---

## Frequently Asked Questions

**Q: Can I commercialize LegalAId?**
A: Yes (MIT License). But if you do, please support upstream development with donations.

**Q: Is LegalAId production-ready?**
A: MVP by June 2025. Beta testing with 3 NGOs. Use at your own risk before 1.0.0.

**Q: How accurate is the legal AI?**
A: Never used alone. Always reviewed by qualified Berater:innen. 5-Layer QA + Human-in-the-Loop required.

**Q: Can NGOs host it themselves?**
A: Yes. Docker-based self-hosting supported. #LeaveNoOneBehind offers managed hosting too.

**Q: What languages are supported?**
A: MVP: German + 9 others (Arabic, Turkish, Farsi, Ukrainian, Russian, Somali, Albanian, Serbian, Tigrinya).

**Q: Is it free?**
A: Yes. MIT License. Code is free. Deployment is your cost (or free via Railway/Render).

---

## Contact & Support

- **GitHub**: N.N.
- **Email**: tjiokdave@gmail.com
- **Discord**: [Link coming soon]
- **Website**: [Link coming soon]

---

**Join us in democratizing legal knowledge for migration counseling! 🚀**

*Last Updated: December 2025*
*Status: Community Building Phase*
