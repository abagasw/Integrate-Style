# 🎨 Design Token System

Sistem Design Token yang powerful menggunakan Style Dictionary untuk mengelola dan mendistribusikan design tokens ke berbagai platform dan format.

[![GitHub Pages](https://img.shields.io/badge/demo-GitHub%20Pages-blue)](https://yourusername.github.io/your-repo-name/demo.html)
[![npm version](https://img.shields.io/badge/npm-v1.0.0-green)](package.json)
[![License](https://img.shields.io/badge/license-ISC-blue)](LICENSE)

## 📋 Daftar Isi

- [Fitur Utama](#-fitur-utama)
- [Instalasi](#-instalasi)
- [Cara Penggunaan](#-cara-penggunaan)
- [Struktur Project](#-struktur-project)
- [Format Output](#-format-output)
- [Integrasi Figma](#-integrasi-figma)
- [Deployment](#-deployment)
- [Pengembangan](#-pengembangan)

## ✨ Fitur Utama

- 🎯 **Multi-Platform Output**: CSS, SCSS, JavaScript, JSON, TypeScript
- 🔄 **Sinkronisasi Figma**: Integrasi dengan Token Studio for Figma
- 🚀 **Auto Deployment**: GitHub Actions untuk build dan deploy otomatis
- 🎨 **Utility Classes**: Generate CSS utility classes otomatis
- 📱 **Responsive**: Konversi px ke rem otomatis
- ☁️ **CDN Ready**: Deploy ke Cloudflare Pages

## 🚀 Instalasi

### Prerequisites
- Node.js (v14 atau lebih tinggi)
- npm atau yarn

### Setup Project

```bash
# Clone repository
git clone <repository-url>
cd design-token-system

# Install dependencies
npm install

# Build tokens pertama kali
npm run build
```

## 🎯 Cara Penggunaan

### 1. CDN Import (Termudah)

Tambahkan baris ini ke CSS atau HTML untuk langsung menggunakan semua design tokens:

```css
@import url("https://cdn.jsdelivr.net/gh/MIICollaboration/design-token-system@main/dist/css/colors-basic/variables.css");
```

**Penggunaan di HTML:**
```html
<head>
    <style>
        @import url("https://cdn.jsdelivr.net/gh/MIICollaboration/design-token-system@main/dist/css/colors-basic/variables.css");
        
        body {
            background: var(--global-primary);
            color: var(--global-white);
        }
    </style>
</head>
```

### 2. Mengelola Tokens

Tokens disimpan dalam folder `tokens/` dengan format JSON:

```json
{
  "global": {
    "primary": {
      "$type": "color",
      "$value": "#FF0025"
    },
    "spacing": {
      "md": {
        "$type": "spacing",
        "$value": "16"
      }
    }
  }
}
```

### 3. Build Tokens

```bash
# Build semua tokens
npm run build

# Build dan bersihkan output sebelumnya
npm run build:clean

# Preview hasil di browser
npm run dev
```

### 4. Menggunakan Output

#### CSS Variables
```css
/* Import CSS variables */
@import url('./dist/css/colors-basic/variables.css');

.my-component {
  background-color: var(--global-primary);
  padding: var(--global-spacing-md);
}
```

#### CSS Utility Classes
```html
<!-- Gunakan utility classes yang di-generate otomatis -->
<div class="bg-global-primary p-global-spacing-md">
  Content dengan design tokens
</div>
```

#### JavaScript/TypeScript
```javascript
// Import tokens sebagai JavaScript object
import tokens from './dist/js/colors-basic/tokens.js';

const primaryColor = tokens.global.primary;
```

#### SCSS Variables
```scss
// Import SCSS variables
@import './dist/scss/colors-basic/variables';

.component {
  background-color: $global-primary;
  padding: $global-spacing-md;
}
```

## 📁 Struktur Project

```
design-token-system/
├── tokens/                    # Source tokens (JSON)
│   ├── colors-basic.json
│   ├── spacing-basic.json
│   ├── figma-tokens.json
│   └── *-converted.json       # Converted tokens
├── dist/                      # Generated output
│   ├── css/                   # CSS variables & utilities
│   │   ├── colors-basic/
│   │   ├── spacing-basic/
│   │   └── figma-tokens/
│   ├── scss/                  # SCSS variables
│   ├── js/                    # JavaScript/TypeScript
│   └── json/                  # JSON format
├── .github/workflows/         # GitHub Actions
├── build.js                   # Build script
├── sync-tokens.js            # Figma sync script
├── config.json               # Style Dictionary config
└── demo.html                 # Demo page
```

## 🎨 Format Output

### CSS Variables
```css
:root {
  --global-primary: #FF0025;
  --global-spacing-md: 1rem;
}
```

### CSS Utility Classes
```css
/* Color utilities */
.bg-global-primary { background-color: var(--global-primary); }
.text-global-primary { color: var(--global-primary); }

/* Spacing utilities */
.p-global-spacing-md { padding: var(--global-spacing-md); }
.pt-global-spacing-md { padding-top: var(--global-spacing-md); }
```

### JavaScript/TypeScript
```javascript
export default {
  global: {
    primary: "#FF0025",
    spacing: {
      md: "1rem"
    }
  }
};
```

### SCSS Variables
```scss
$global-primary: #FF0025;
$global-spacing-md: 1rem;
```

## 🎭 Integrasi Figma

### Setup Token Studio

1. **Install Plugin**
   - Buka Figma
   - Install "Figma Tokens" plugin

2. **Connect Repository**
   - Pilih GitHub sebagai sync provider
   - Repository: `your-username/design-token-system`
   - Branch: `main`
   - File path: `figma-tokens.json`

3. **Sync Tokens**
   ```bash
   # Sync dari Figma ke Style Dictionary
   npm run sync:from-figma
   
   # Sync dari Style Dictionary ke Figma
   npm run sync:to-figma
   ```

### Workflow Figma

1. **Figma → Code**:
   - Edit tokens di Figma Token Studio
   - Push ke GitHub dari plugin
   - GitHub Actions otomatis build dan deploy

2. **Code → Figma**:
   - Edit file JSON di `tokens/`
   - Run `npm run sync:to-figma`
   - Pull dari GitHub di Figma Token Studio

## 🚀 Deployment

### GitHub Pages (Otomatis)

Setiap push ke `main` branch akan otomatis:
1. Build semua tokens
2. Deploy ke GitHub Pages
3. Update CDN links

### Cloudflare Pages

1. **Setup Secrets**:
   ```bash
   # Set GitHub secrets
   CLOUDFLARE_API_TOKEN=your_token
   CLOUDFLARE_ACCOUNT_ID=your_account_id
   ```

2. **Deploy Manual**:
   ```bash
   npm run build
   # Upload dist/ ke Cloudflare Pages
   ```

## 🛠 Pengembangan

### Menambah Token Baru

1. **Edit file JSON** di `tokens/`:
   ```json
   {
     "global": {
       "newColor": {
         "$type": "color",
         "$value": "#123456"
       }
     }
   }
   ```

2. **Build ulang**:
   ```bash
   npm run build
   ```

### Custom Transforms

Edit `build.js` untuk menambah transform custom:

```javascript
StyleDictionary.registerTransform({
  name: 'custom/transform',
  type: 'value',
  matcher: function(token) {
    return token.type === 'custom';
  },
  transformer: function(token) {
    return `custom-${token.value}`;
  }
});
```

### Custom Formats

Tambah format output baru:

```javascript
StyleDictionary.registerFormat({
  name: 'custom/format',
  formatter: function(dictionary) {
    return dictionary.allTokens
      .map(token => `${token.name}: ${token.value}`)
      .join('\n');
  }
});
```

## 📚 Scripts Available

```bash
npm run build          # Build semua tokens
npm run build:clean    # Clean + build
npm run dev           # Build + open demo
npm run sync:from-figma # Sync dari Figma
npm run sync:to-figma   # Sync ke Figma
```

## 🎨 Token Categories

### Colors
- **Brand Colors**: Primary, secondary
- **Neutral Colors**: White, black, gray scale (50-900)

### Spacing
- **Scale**: xs (4px) → 2xl (48px)
- **Usage**: Padding, margins, gaps

### Border Radius
- **Scale**: none, sm, md, lg, full
- **Usage**: Rounded corners

### Typography
- **Font Sizes**: xs → 4xl
- **Font Weights**: normal, semibold, bold
- **Line Heights**: tight, normal, relaxed

## 🤝 Contributing

1. Fork repository
2. Buat feature branch
3. Commit changes
4. Push ke branch
5. Buat Pull Request

## 📄 License

ISC License - lihat file LICENSE untuk detail.

## 🆘 Troubleshooting

### Build Error
```bash
# Clear node_modules dan reinstall
rm -rf node_modules package-lock.json
npm install
npm run build
```

### Figma Sync Issues
- Pastikan Personal Access Token memiliki repo permissions
- Check file path di Token Studio settings
- Verify branch name (main/master)

### CDN Cache Issues
- Gunakan versioned URLs: `@main` atau `@v1.0.0`
- Clear browser cache
- Wait for CDN propagation (5-10 menit)

---

**Happy Designing! 🎨✨**
