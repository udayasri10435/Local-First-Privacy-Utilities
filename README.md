# README.md — Privacy-First Utility Apps (WebAssembly)

<div align="center">
  <img src="public/assets/logo.svg" alt="Privacy-First Utilities Logo" width="200"/>
  <br/>
  <strong>🔒 Process sensitive data entirely in your browser. No uploads. No servers. No tracking.</strong>
</div>

<br/>

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![WebAssembly](https://img.shields.io/badge/WebAssembly-654FF0?logo=webassembly&logoColor=white)](https://webassembly.org/)
[![React](https://img.shields.io/badge/React-20232A?logo=react&logoColor=61DAFB)](https://reactjs.org/)
[![Vite](https://img.shields.io/badge/Vite-646CFF?logo=vite&logoColor=white)](https://vitejs.dev/)

---

## 📋 Table of Contents
- [✨ Features](#-features)
- [📦 Apps](#-apps)
- [🚀 Quick Start](#-quick-start)
- [📁 Project Structure](#-project-structure)
- [🛠️ Tech Stack](#️-tech-stack)
- [🔒 Privacy Guarantees](#-privacy-guarantees)
- [📖 Documentation](#-documentation)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)
- [🙏 Acknowledgments](#-acknowledgments)

---

## ✨ Features

- **🔐 Zero Data Transmission** — All processing happens client-side. Nothing ever hits a server.
- **⚡ WebAssembly Power** — High-performance computation using compiled C++/Rust code in your browser.
- **🎯 Pattern Matching** — Auto-detect sensitive information like emails, phone numbers, or custom regex patterns.
- **🌺 Intuitive UI** — Serene, minimalist interfaces that make complex operations simple.
- **💾 Local-First** — Files and data persist only in your browser's memory and storage.
- **🔑 Cryptographic Security** — Industry-standard encryption (AES-256-GCM) and Shamir's Secret Sharing.

---

## 📦 Apps

### 1. 📄 Local-Only Document Redactor

A PDF and Word document viewer where you highlight text to redact. Uses OpenCV compiled to WebAssembly to physically destroy pixels and text vectors in browser memory.

<div align="center">
  <img src="public/assets/redactor-screenshot.png" alt="Document Redactor Screenshot" width="600"/>
</div>

**Key Features:**
- **Pattern Match Auto-Redaction** — Upload a list of emails/terms; they're auto-highlighted for redaction.
- **Physical Data Destruction** — Permanent pixel-level removal, not just overlay.
- **Multiple Formats** — Supports PDF, DOCX, and image-based documents.
- **Real-Time Preview** — See redactions before applying them.

**Tech Stack:** OpenCV (Wasm via Emscripten), PDF-lib, Mammoth.js, React

---

### 2. 🌺 Digital Inheritance Vault

Encrypted, time-locked message storage with a "heartbeat" check-in system. If you miss your check-in (e.g., 30 days), decryption keys are slowly released to recipients via Shamir's Secret Sharing.

<div align="center">
  <img src="public/assets/vault-screenshot.png" alt="Digital Inheritance Vault Screenshot" width="600"/>
</div>

**Key Features:**
- **Shamir's Secret Sharing** — Keys split into shares requiring threshold collaboration to reconstruct.
- **Dead Man's Switch** — Progressive escalation: alerts → contacts notified → voting → release.
- **"Garden" UI** — Each key share is a flower that blooms as release approaches.
- **Zero-Knowledge** — Server never sees plaintext or reconstructed keys.

**Tech Stack:** WebCrypto API (AES-256-GCM), Shamir's Secret Sharing library, React, Framer Motion

---

## 🚀 Quick Start

### Prerequisites
- Node.js (v16 or higher)
- npm or yarn

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/privacy-utils.git
cd privacy-utils

# Install dependencies
npm install

# Start development server
npm run dev

# Open your browser at http://localhost:5173
```

### Build for Production

```bash
# Build the application
npm run build

# Preview production build
npm run preview
```

### Docker (Optional)

```bash
# Build Docker image
docker build -t privacy-utils .

# Run container
docker run -p 80:80 privacy-utils
```

---

## 📁 Project Structure

```
privacy-utils/
├── src/
│   ├── redactor/                    # Document Redactor
│   │   ├── components/              # UI components
│   │   │   ├── PDFViewer.tsx
│   │   │   ├── PatternList.tsx
│   │   │   └── RedactionToolbar.tsx
│   │   ├── services/                # Core logic
│   │   │   ├── opencv-loader.ts     # Wasm OpenCV initialization
│   │   │   ├── pdf-processor.ts     # PDF parsing & redaction
│   │   │   └── pattern-match.ts     # Auto-redaction engine
│   │   └── hooks/                   # React hooks
│   │       └── useRedactor.ts
│   ├── vault/                       # Digital Inheritance Vault
│   │   ├── components/              # UI components
│   │   │   ├── Garden.tsx
│   │   │   ├── Flower.tsx
│   │   │   └── HeartbeatMonitor.tsx
│   │   ├── services/                # Core logic
│   │   │   ├── shamir.ts            # Secret splitting/reconstruction
│   │   │   ├── heartbeat.ts         # Check-in monitoring
│   │   │   └── encryption.ts        # AES-256-GCM encryption
│   │   └── hooks/                   # React hooks
│   │       └── useVault.ts
│   ├── common/                      # Shared utilities
│   │   ├── crypto/                  # Cryptographic helpers
│   │   ├── storage/                 # LocalStorage/IndexedDB
│   │   └── types/                   # TypeScript definitions
│   ├── App.tsx
│   └── main.tsx
├── wasm/                            # WebAssembly builds
│   └── opencv/
│       ├── build.sh                 # Emscripten build script
│       └── opencv.js/               # Compiled output
├── public/
│   └── assets/
│       ├── logo.svg
│       └── screenshots/
├── tests/                           # Unit and integration tests
│   ├── redactor/
│   └── vault/
├── .env.example
├── .gitignore
├── Dockerfile
├── index.html
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README.md
```

---

## 🛠️ Tech Stack

| Category | Technology | Purpose |
|----------|------------|---------|
| **Framework** | React 18 + Vite | UI & build tool |
| **Language** | TypeScript | Type safety |
| **Styling** | TailwindCSS + Framer Motion | UI & animations |
| **Image Processing** | OpenCV (WebAssembly) | Pixel-level document manipulation |
| **Document Parsing** | PDF-lib, Mammoth.js | PDF/DOCX parsing |
| **Cryptography** | WebCrypto API, Shamir.js | Encryption & secret sharing |
| **Storage** | IndexedDB, LocalStorage | Client-side data persistence |
| **Testing** | Vitest + React Testing Library | Unit & integration tests |
| **CI/CD** | GitHub Actions | Automated builds & deployments |
| **Container** | Docker | Containerization |

---

## 🔒 Privacy Guarantees

| Guarantee | Implementation |
|-----------|----------------|
| **No Data Transmission** | All API calls blocked; only static assets served |
| **Local Processing** | WebAssembly executes entirely in browser |
| **Memory Isolation** | Files stored only in browser memory (not persisted) |
| **No Logs** | Zero telemetry, analytics, or error tracking |
| **No Tracking** | No cookies, fingerprinting, or localStorage tracking |
| **Encrypted Storage** | All persisted data encrypted with AES-256-GCM |
| **Client-Only Keys** | Cryptographic keys never leave the client |

---

## 📖 Documentation

### User Guides
- [Document Redactor User Guide](docs/redactor-guide.md)
- [Digital Inheritance Vault User Guide](docs/vault-guide.md)
- [FAQ](docs/faq.md)

### Developer Docs
- [WebAssembly Build Guide](docs/wasm-build.md)
- [API Reference](docs/api.md)
- [Architecture Overview](docs/architecture.md)
- [Security Audit](docs/security.md)

### External References
- [OpenCV.js Documentation](https://docs.opencv.org/4.5.3/d5/d10/tutorial_js_root.html)
- [Shamir's Secret Sharing](https://en.wikipedia.org/wiki/Shamir%27s_Secret_Sharing)
- [WebCrypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API)
- [WebAssembly Concepts](https://webassembly.org/docs/)

---

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md).

### Development Workflow

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to your branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### Code Style
- ESLint + Prettier for code formatting
- Conventional Commits for commit messages
- TypeScript for all new code

### Testing
```bash
# Run tests
npm test

# Run tests with coverage
npm run test:coverage

# Run e2e tests
npm run test:e2e
```

---

## 🐛 Reporting Issues

Please report bugs and feature requests using the [GitHub Issue Tracker](https://github.com/yourusername/privacy-utils/issues).

**Template for bugs:**
- OS and browser version
- Steps to reproduce
- Expected vs actual behavior
- Screenshots (if applicable)

---

## 📄 License

Distributed under the MIT License. See [LICENSE](LICENSE) for more information.

---

## 🙏 Acknowledgments

- **[OpenCV](https://opencv.org/)** — Computer vision library compiled to WebAssembly
- **[Shamir's Secret Sharing](https://github.com/dsprenkels/sss)** — Cryptographic splitting algorithm
- **[Afterkey](https://github.com/bonkai/afterkey)** — Inspiration for dead man's switch design
- **[Vault12](https://vault12.com/)** — Production Shamir's Secret Sharing implementation
- **[WebAssembly Community](https://webassembly.org/)** — Making local-first computing possible

---

## 🌟 Star History

[![Star History Chart](https://api.star-history.com/svg?repos=yourusername/privacy-utils&type=Date)](https://star-history.com/#yourusername/privacy-utils&Date)

---

## 📞 Contact

- **GitHub Issues**: [Submit here](https://github.com/yourusername/privacy-utils/issues)
- **Email**: privacy-utils@example.com
- **Twitter**: [@privacy_utils](https://twitter.com/privacy_utils)

---

<div align="center">
  <sub>Built with ❤️ for privacy. Runs on trust—not servers.</sub>
  <br/>
  <sub>⭐ If this project helps you, please give it a star!</sub>
</div>
