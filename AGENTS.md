# AGENTS.md — Theme TKKP (theme_tkkp)

## Ringkasan Plugin

| Field          | Nilai                                       |
|----------------|---------------------------------------------|
| Nama plugin    | `theme_tkkp`                                |
| Tipe plugin    | Theme (Moodle theme plugin)                 |
| Versi          | 0.0.1                                       |
| Target Moodle  | Moodle 4.5+                                 |
| Parent theme   | `boost` (Bootstrap 5)                       |
| Lisensi        | GPL-3.0+                                    |
| Author         | Yohan Naftali — https://yohanli.com         |

## Struktur Direktori

```
theme/tkkp/
├── config.php                  # Konfigurasi utama tema
├── lib.php                     # Fungsi PHP tema (SCSS compile, file serving)
├── Gruntfile.js                # Build task (uglify, eslint, stylelint, watch)
├── package.json                # Node.js dev dependencies
├── LICENSE.md
├── fonts/
│   └── OpenDyslexic-*/         # Font OpenDyslexic (.eot, .otf, .woff, .woff2)
├── lang/
│   └── en/
│       └── theme_tkkp.php      # String bahasa (English)
├── pix/
│   └── favicon.ico             # Favicon default
├── scss/
│   ├── default.scss            # Entry point SCSS (import semua partial)
│   ├── extras/
│   │   └── _opendyslexic.scss  # Stylesheet font OpenDyslexic
│   └── tkkp/
│       ├── _variables.scss     # Variabel warna & brand
│       ├── _general.scss       # Style umum & body
│       ├── _transitions.scss   # Transisi CSS
│       ├── _pages.scss         # Layout halaman
│       ├── _blocks.scss        # Styling blok Moodle
│       ├── _drawers.scss       # Sidebar/drawer kiri & kanan
│       ├── _navbar.scss        # Navigation bar atas
│       ├── _footer.scss        # Footer halaman
│       ├── _breadcrumb.scss    # Breadcrumb navigasi
│       ├── _course.scss        # Tampilan halaman kursus
│       ├── _login.scss         # Halaman login
│       ├── _mydashboard.scss   # Halaman dashboard pengguna
│       ├── _frontpage.scss     # Halaman depan (frontpage)
│       ├── _profile.scss       # Profil pengguna
│       ├── _enrol.scss         # Pendaftaran kursus
│       ├── _accessibilitybar.scss    # Accessibility toolbar
│       ├── _accessibilitystyles.scss # Gaya saat accessibility aktif
│       ├── _buttons.scss       # Tombol
│       ├── _labels.scss        # Label
│       ├── _security.scss      # Override keamanan CSS
│       └── mixins/
│           └── _accessibilityfontsize.scss  # Mixin ukuran font accessibility
├── style/
│   └── moodle.css              # CSS pre-compiled (fallback)
└── templates/
    ├── accessibilitybar.mustache           # Toolbar aksesibilitas
    ├── accessibilitysettings_modal.mustache
    ├── head.mustache                       # Tag <head> HTML
    ├── navbar.mustache                     # Navigation bar
    ├── footer.mustache                     # Footer
    ├── drawers.mustache                    # Layout utama dengan drawer
    ├── frontpage.mustache                  # Layout halaman depan
    ├── login.mustache                      # Layout halaman login
    ├── course.mustache                     # Layout halaman kursus
    ├── incourse.mustache                   # Layout dalam kursus
    ├── mypublic.mustache                   # Profil publik pengguna
    ├── language_menu.mustache              # Menu pilihan bahasa
    ├── moove_coursecard.mustache           # Card kursus (moove-style)
    ├── primary-drawer-mobile.mustache      # Drawer mobile
    ├── core/
    │   ├── full_header.mustache            # Override header utama
    │   ├── loginform.mustache              # Override form login
    │   ├── user_menu.mustache              # Override menu pengguna
    │   └── welcome.mustache               # Override pesan selamat datang
    ├── core_course/
    │   ├── activity_navigation.mustache    # Override navigasi aktivitas
    │   └── coursecard.mustache            # Override card kursus
    ├── core_message/
    │   └── message_popover.mustache        # Override popover pesan
    ├── block_myoverview/
    │   ├── course-action-menu.mustache     # Override menu aksi kursus
    │   ├── progress-bar.mustache           # Override progress bar
    │   └── view-cards.mustache            # Override tampilan card
    └── message_popup/
        └── notification_popover.mustache   # Override popover notifikasi
```

## Arsitektur Tema

### Pewarisan (Inheritance)
- Parent theme: `boost` — semua layout, JS, dan SCSS Boost diwarisi secara default.
- Template Mustache menggunakan namespace `theme_moove/` pada beberapa partial (drawers, navbar, footer, dll.) karena tema ini terinspirasi/di-fork dari tema [Moove](https://moodle.org/plugins/theme_moove).

### SCSS Build
Fungsi PHP di `lib.php` yang mengelola SCSS:
- `theme_tkkp_get_pre_scss()` — inject variabel brand color, secondary menu color, font sebelum Boost SCSS.
- `theme_tkkp_get_main_scss_content()` — load preset Boost + variabel tkkp + SCSS utama + security overrides.
- `theme_tkkp_get_extra_scss()` — tambahan SCSS dari admin + background login.
- `theme_tkkp_get_precompiled_css()` — fallback CSS dari `style/moodle.css`.

### Variabel SCSS Utama (`scss/tkkp/_variables.scss`)
| Variabel               | Default      | Keterangan                     |
|------------------------|--------------|--------------------------------|
| `$brand-primary`       | `#0f47ad`    | Warna utama brand              |
| `$green`               | `#64a44e`    | Aksen hijau                    |
| `$gold`                | `#f7bf29`    | Aksen emas                     |
| `$background`          | `#f2f3f7`    | Warna background body          |
| `$secondary-menu-color`| `$brand-primary` | Warna menu sekunder        |

### Fitur Aksesibilitas
- **Accessibility Bar**: toolbar fixed-top untuk mengatur ukuran font (A- / A / A+) dan warna situs.
- **Font OpenDyslexic**: font opsional untuk pengguna disleksia, tersedia dalam `fonts/` dan `scss/extras/_opendyslexic.scss`.

### File Serving
`theme_tkkp_pluginfile()` melayani file di area: `logo`, `loginbgimg`, `favicon`, `sliderimage[1-9][0-9]?`, `marketing1icon` s.d. `marketing4icon`.

## Konvensi Pengembangan

### Penambahan Style Baru
1. Buat file partial baru di `scss/tkkp/_namafile.scss`.
2. Import di `scss/default.scss` sesuai urutan logis.
3. Gunakan variabel dari `_variables.scss`, jangan hardcode warna.

### Penambahan Template
1. Buat file `.mustache` di `templates/` sesuai struktur namespace Moodle.
2. Untuk override template core, tempatkan di `templates/core/` atau `templates/core_course/` dll.
3. Perhatikan namespace `theme_moove/` pada partial yang ada — jangan ubah tanpa memastikan kompatibilitas.

### Build Tools
```bash
npm install          # Install dev dependencies
grunt                # Watch mode (default)
grunt amd            # Compile AMD JS
grunt css            # Lint SCSS & CSS
grunt decache        # Purge Moodle cache via CLI
grunt compile        # Compile + purge cache
```

### Struktur Commit
Gunakan format: `[tipe]: deskripsi singkat`
- `feat:` fitur baru
- `fix:` perbaikan bug
- `style:` perubahan CSS/SCSS tanpa logika
- `refactor:` refaktor kode
- `docs:` dokumentasi

## Catatan Penting

- Template yang memakai `{{> theme_moove/...}}` bergantung pada namespace Moove karena asal-usul fork. Pastikan Moove tersedia atau ganti namespace ke `theme_tkkp` saat migrasi penuh.
- File `style/moodle.css` adalah fallback statis; perbarui setelah mengubah SCSS.
- Pengaturan `$THEME->usefallback = true` di `config.php` mengaktifkan fallback ke CSS statis jika SCSS compile gagal.
