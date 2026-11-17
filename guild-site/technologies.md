# The Wyrm Hunters --- Technical Requirements

## 1. Project Overview

**Project:** The Wyrm Hunters\
**Website type:** Responsive, single-page guild landing page\
**Frontend framework:** Angular\
**Visual direction:** Premium dark medieval fantasy

**Primary goals:** - Present the guild, its services, completed
contracts, clients, and hunters. - Establish credibility through
testimonials and completed work. - Allow visitors to submit a contract
request. - Provide a fast, accessible, search-engine-friendly experience
on desktop and mobile devices.

Prioritize maintainable components, clear separation of concerns,
performance, accessibility, and visual consistency.

## 2. Frontend Framework

### Angular

Use Angular as the primary frontend framework.

Requirements: - Use a current stable Angular release at project
initialization. - Use standalone components and the modern Angular
application structure. - Use Angular Router only if the project grows
beyond the initial landing page or needs separate routes. - Keep
components focused and reusable. - Separate presentation components from
data and service logic. - Use TypeScript with strict type checking. -
Avoid unnecessary dependencies and oversized UI frameworks.

Suggested component structure: - `HeaderComponent` - `HeroComponent` -
`ServicesComponent` - `CompletedContractsComponent` -
`TestimonialsComponent` - `HuntersComponent` - `ContactFormComponent` -
`FooterComponent`

Reusable components may include buttons, section headings, cards,
badges, and decorative separators.

## 3. CSS and Styling

### Tailwind CSS

Use Tailwind CSS for layout, spacing, responsive behavior, typography,
and most component styling.

Reasons: - Works with Angular. - Allows precise control over a custom
visual identity. - Avoids imposing a predefined component-library
appearance. - Makes responsive layouts and consistent spacing easier to
maintain.

Use the current Tailwind CSS integration documented for Angular. Do not
copy setup instructions from older Tailwind v3 tutorials when
configuring a new project.

### Custom CSS

Use component-level CSS or global CSS only where it provides a clear
benefit, for example: - Complex decorative borders and heraldic
frames. - Custom animations and transitions. - Fine-grained
typography. - Background textures and layered visual effects. -
Third-party component overrides.

Define the brand palette as reusable CSS variables or Tailwind theme
tokens. Do not scatter raw color values throughout templates.

Do not add Angular Material, Bootstrap, or another large UI framework
unless a specific requirement justifies it.

## 4. Responsive and Adaptive Design

The website must be fully responsive.

Required target layouts: - Mobile: approximately 320--767 px. - Tablet:
approximately 768--1023 px. - Desktop: 1024 px and wider.

Requirements: - Use a mobile-first approach. - Avoid horizontal page
overflow. - Adapt navigation for narrow screens. - Reflow multi-column
sections into one column on mobile. - Adjust typography, spacing, card
dimensions, and image crops at different viewport widths. - Keep buttons
and interactive targets comfortable to use on touch screens. - Ensure
forms remain usable on narrow screens. - Support portrait and landscape
mobile orientations. - Do not rely on hover interactions for essential
functionality.

Test at common viewport sizes, including 360 px, 390 px, 768 px, 1024
px, 1440 px, and wider desktop screens.

## 5. Contact Form and API Integration

### Initial implementation

The contact form must work against a mock API service until a real
backend or messaging provider is selected.

Do not couple the form component directly to a specific email or
messaging provider.

Create an abstraction such as: - `ContractRequestService` -
`ContractRequestApi` - `MockContractRequestApi`

The form should submit a typed request model through the service. The
mock implementation should simulate network latency and return success
or failure responses so that loading, success, and error states can be
implemented and tested.

### Future delivery options

**Preferred public contact channel:** Email delivery through a backend
endpoint or serverless function.

**Optional internal notification:** Telegram bot notification to the
guild operators.

A Telegram bot may be useful for immediate internal notifications, but
it should not be treated as a public form endpoint by itself.

Security requirements: - Never expose a Telegram bot token,
email-provider API key, or other secret in frontend code. - Send
messages through a backend endpoint or serverless function. - Validate
all submitted data on the server, even if client-side validation is also
present. - Add spam protection before public launch, such as rate
limiting and a suitable CAPTCHA or honeypot. - Do not log sensitive form
content unnecessarily.

### Form behavior

The form must include: - Required-field validation. - Email format
validation. - Clear field-level validation messages. -
Submission/loading state. - Success confirmation. - Error state with a
retry option. - Protection against accidental duplicate submissions.

The UI should remain unchanged when the delivery provider is replaced.

## 6. Carousels and Sliders

### Library

Swiper, using Swiper Element (Web Components) with Angular.

Use a maintained, established carousel library rather than implementing
slide movement, touch handling, looping, and responsive behavior from
scratch.

Official documentation: - https://swiperjs.com/ -
https://swiperjs.com/swiper-api

Swiper provides loop mode, autoplay, navigation, pagination, touch
interaction, and accessibility-related functionality. When integrating
it with Angular SSR, initialize browser-dependent behavior only on the
client after rendering/hydration, and verify that it does not cause
hydration mismatches.

### Testimonials carousel behavior

The testimonials section contains approximately ten client testimonials.

Recommended initial settings: - Autoplay delay: **5,500 ms**. -
Transition duration: **450--600 ms**. - Continuous loop: enabled. -
Navigation: previous and next controls. - Pagination: optional
indicators, if they fit the design. - Touch and mouse dragging: enabled
where appropriate. - Responsive slides per view: adapt to the available
width. - Pause autoplay while the pointer is over the carousel. - Pause
autoplay while a control or slide has keyboard focus. - Stop or pause
autoplay when the browser tab is hidden. - Respect the user's
`prefers-reduced-motion` setting; disable automatic movement when
reduced motion is requested.

Autoplay must never prevent manual navigation. After manual interaction,
the carousel may resume automatically, provided it remains accessible
and does not surprise the user.

Do not use a very fast rotation. Testimonials need enough time to be
read comfortably.

### Other carousels

Use the same library for other carousel sections if they are introduced.
Configure each instance according to its content; do not force every
carousel to use identical settings.

## 7. Rendering, SSR, and SEO

### Angular SSR and prerendering

Enable Angular's official SSR and hybrid-rendering support.

Because the initial website is primarily static marketing content,
prefer **prerendering / static site generation (SSG)** for stable public
sections when practical. Use server-side rendering for routes or content
that genuinely needs request-time data.

Enable Angular hydration and verify that interactive components work
correctly after hydration.

Requirements: - The main page content must be present in the initial
HTML. - Avoid browser-only APIs during server rendering. - Initialize
browser-dependent libraries only in the browser. - Avoid hydration
mismatches and layout shifts. - Keep the page usable if a non-essential
animation or carousel fails to initialize.

Official documentation: - https://angular.dev/guide/ssr -
https://angular.dev/guide/hydration -
https://angular.dev/guide/routing/rendering-strategies

### SEO

Implement: - Unique page title. - Meta description. - Canonical URL. -
Open Graph metadata for social sharing. - Appropriate Twitter/X card
metadata. - Semantic HTML structure with one clear main heading (`h1`)
and correctly nested section headings. - Descriptive image `alt` text. -
`robots.txt`. - XML sitemap. - Correct favicon and web app icons. -
Meaningful page URL and domain configuration.

Use Angular's title and meta facilities to manage metadata.

Add structured data only when it accurately describes the real website
and its content. Do not add fake ratings, reviews, addresses, or
organization details as SEO markup.

## 8. Performance and Image Handling

The website will contain multiple generated illustrations and character
portraits. Image performance is therefore important.

Requirements: - Use modern image formats such as AVIF or WebP where
supported. - Provide appropriate image dimensions and responsive
variants. - Avoid loading full-resolution source images when smaller
versions are sufficient. - Lazy-load below-the-fold images. - Prioritize
the hero image if it is important to the initial visual presentation. -
Reserve image dimensions or aspect ratios to prevent layout shifts. -
Avoid unnecessary background video and heavy animation. - Minimize
JavaScript and third-party dependencies. - Use production builds and
appropriate asset caching.

Do not lazy-load the main above-the-fold hero image if doing so delays
the initial visual presentation.

## 9. Accessibility

The site should follow WCAG 2.2 AA principles where practical.

Requirements: - Use semantic HTML elements. - Ensure sufficient text and
control contrast. - Provide visible keyboard focus indicators. - Support
keyboard navigation. - Add accessible labels to form fields and
controls. - Provide meaningful alternative text for informative
images. - Use empty `alt` text for purely decorative images. - Do not
communicate status using color alone. - Respect reduced-motion
preferences. - Ensure carousel controls are keyboard-accessible and have
accessible names. - Do not make essential content available only through
hover.

## 10. Testing and Code Quality

Requirements: - Enable TypeScript strict mode. - Use Angular's supported
testing setup. - Add unit tests for important services and form
validation. - Test contact form success, validation, failure, and
duplicate-submit behavior. - Test carousel behavior at mobile and
desktop widths. - Verify SSR/prerender output and hydration in a
production build. - Check the site in current versions of Chrome,
Firefox, Safari, and Edge where available. - Run accessibility checks
and fix major issues. - Avoid unnecessary abstractions and dependencies.

## 11. Security and Configuration

Requirements: - Keep secrets and API credentials on the server. - Use
HTTPS in production. - Validate and sanitize untrusted form input on the
backend. - Configure appropriate security headers on the hosting/server
layer. - Keep dependencies updated and review security advisories. -
Store environment-specific configuration outside source-controlled
secrets. - Do not expose internal error details to website visitors.

## 7. Internationalization (i18n)

### ngx-translate

Use **ngx-translate v18** for runtime language switching.

ngx-translate remains actively maintained. Version 18 is the current
supported major version and supports Angular 18--22. Use a compatible
current v18 release when setting up the project; do not use the obsolete
v17 or earlier lines.

Official documentation: - https://ngx-translate.org/ -
https://ngx-translate.org/getting-started/angular-compatibility/ -
https://ngx-translate.org/getting-started/translation-files/

Use the modern standalone provider API (`provideTranslateService`) and
standalone translation pipe/directive. Do not use the removed
`TranslateModule.forRoot()` API from older tutorials.

### Supported Languages

The initial website must support:

  Language   Identifier   Role
  ---------- ------------ -------------------------------
  English    `en`         Primary language and fallback
  Quenya     `qya`        Additional language

The Quenya identifier `qya` is the ISO 639-3 code for Quenya. Use it
consistently as the ngx-translate language key and translation-file
name.

Quenya is a constructed language. Translation content must be reviewed
for grammar, vocabulary, and spelling consistency; do not rely on
unreviewed machine translation for the final public copy.

### Translation Files

Store translations as separate JSON files in the public translation
directory.

Suggested structure:

``` text
public/
  i18n/
    en.json
    qya.json
```

Requirements: - Use stable, descriptive translation keys grouped by page
section or component. - Keep the same key structure in every language
file. - English must contain the complete set of keys and act as the
fallback language. - Do not use visible English sentences as translation
keys. - Keep translations separate from component templates and
application logic. - Handle missing translation keys gracefully and
report them during development. - Load translation files through the
ngx-translate HTTP loader or another suitable loader.

Example key organization:

``` json
{
  "navigation": {
    "about": "About",
    "services": "Services",
    "hunters": "The Hunters",
    "contact": "Request a Hunter"
  },
  "hero": {
    "title": "The Wyrm Hunters",
    "slogan": "We Hunt. You Rest."
  }
}
```

The example above illustrates the English key structure. The Quenya file
must use the same keys with Quenya values.

### Language Switcher

Add a language selector to the main navigation.

Requirements: - Allow switching between English and Quenya without
reloading the page. - Clearly indicate the currently selected
language. - Use language names in their own language where
appropriate. - Persist the user's selection across visits, for example
with local storage. - On first visit, use English unless a reliable
language preference is explicitly configured. - If a saved language is
unavailable or fails to load, fall back to English. - Avoid displaying
untranslated keys while a language file is loading.

### HTML Language and Rendering

-   Keep the document's `<html lang>` attribute synchronized with the
    active language (`en` or `qya`).
-   Ensure the selected language is applied before or during initial
    rendering to avoid a flash of the wrong language.
-   Make the language selection compatible with Angular SSR,
    prerendering, and hydration.
-   For prerendered language variants, generate the appropriate
    localized output for each supported language.
-   If localized routes are used, keep the language in the URL (for
    example `/en/` and `/qya/`) and provide correct canonical and
    language-alternate metadata.
-   Do not assume that Angular's built-in locale data provides Quenya
    date, number, or currency formatting. Keep standard numeric/date
    formatting separate from translated UI strings unless a suitable
    locale implementation is added.

### Translation Quality

-   Keep the guild's established tone in both languages: professional,
    restrained, medieval fantasy, with subtle humor.
-   Translate meaning and tone rather than mechanically translating each
    English word.
-   Preserve names, proper nouns, and established fictional terminology
    consistently.
-   Review all visible text, including navigation, buttons, form labels,
    validation messages, success/error messages, testimonials, service
    descriptions, metadata, and accessibility labels.
-   Do not leave hard-coded user-facing strings in components.
-   Treat the English translation file as the source of truth for the
    complete set of translation keys.

## 13. Suggested Implementation Priorities

### Phase 1 --- Foundation

-   Create the Angular application.
-   Configure Tailwind CSS.
-   Establish the global color tokens and typography.
-   Build the responsive page structure and reusable components.

### Phase 2 --- Interactive UI

-   Implement the testimonials carousel with Swiper.
-   Implement contact form validation and UI states.
-   Connect the form to the mock API service.

### Phase 3 --- Rendering and discoverability

-   Configure prerendering / SSR and hydration.
-   Add page metadata, Open Graph, sitemap, and robots.txt.
-   Verify that the rendered HTML contains the main content.

### Phase 4 --- Quality

-   Optimize images and loading behavior.
-   Test responsive layouts.
-   Run accessibility and performance checks.
-   Verify production build and deployment behavior.

## 14. Official References

-   Angular: https://angular.dev/
-   Angular SSR and hybrid rendering: https://angular.dev/guide/ssr
-   Angular hydration: https://angular.dev/guide/hydration
-   Angular rendering strategies:
    https://angular.dev/guide/routing/rendering-strategies
-   Angular and Tailwind CSS: https://angular.dev/guide/tailwind
-   Tailwind CSS: https://tailwindcss.com/
-   Swiper: https://swiperjs.com/
-   Swiper API: https://swiperjs.com/swiper-api
