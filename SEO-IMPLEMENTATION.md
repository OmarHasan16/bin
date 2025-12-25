# Hugo SEO Implementation Guide for 10Corp

**Last Updated**: December 24, 2025

## Overview
This document outlines the comprehensive SEO enhancements implemented for the 10Corp Hugo site.

---

## 1. Meta Tags Implementation

### Location: `themes/terio/layouts/partials/head.html`

#### Basic SEO Meta Tags
- **Title Tag**: Uses `seoTitle` parameter with fallbacks
- **Meta Description**: Dynamic from frontmatter or site defaults
- **Keywords**: Array format in frontmatter, comma-delimited output
- **Canonical URL**: Automatically generated for each page
- **Robots**: Configurable per page (default: "index, follow")

#### Open Graph Tags
- `og:title`, `og:description`, `og:url`
- `og:type`: Dynamic (article for blog posts, website for others)
- `og:image`: Absolute URLs with secure_url, width, height, alt
- `og:site_name`, `og:locale` with alternates
- **Article-specific tags** for blog posts:
  - `article:published_time`
  - `article:modified_time`
  - `article:author`
  - `article:tag` (from keywords)

#### Twitter Card Tags
- `twitter:card`: summary_large_image
- `twitter:title`, `twitter:description`
- `twitter:image` with alt text
- `twitter:site`, `twitter:creator`

---

## 2. Structured Data (JSON-LD)

### Location: `themes/terio/layouts/partials/schema.html`

### Organization & LocalBusiness Schema
Combined schema includes:
- Basic organization info
- LocalBusiness with address and geo-coordinates
- ProfessionalService classification
- Contact points with multilingual support
- Social media profiles (sameAs)
- Opening hours specification
- Service catalog with offerings

### WebSite Schema (Homepage Only)
- Site name and URL
- Search action with SearchBox for Google
- Publisher information
- Language specification

### BreadcrumbList Schema (Non-Homepage)
- Automatic breadcrumb generation
- Dynamic position tracking
- Humanized section names
- Full path hierarchy

### BlogPosting Schema (Blog Pages)
- Article metadata (headline, description)
- Published and modified dates (ISO 8601)
- Author and publisher information
- Image objects with dimensions
- Keywords array
- Word count and language

### Service Offerings Schema
- ItemList of all service tiers
- Pricing information
- Availability status
- Provider details

### Review Schema
- Customer reviews with ratings
- Schema.org compliant structure

---

## 3. Configuration Settings

### Location: `config.toml`

#### SEO-Specific Settings
```toml
enableRobotsTXT = true
disableHugoGeneratorInject = true
enableGitInfo = false
```

#### Params for SEO
```toml
[params]
  description = "Site-wide default description"
  defaultImage = "/images/logo.png"
  
  # Organization Details
  organization = "10Corp"
  logo = "/images/logo.png"
  telephone = "+17622333344"
  email = "info@10corp.com"
  address = "2709 N Hayden Island Dr. STE 520328"
  addressLocality = "Portland"
  addressRegion = "Oregon"
  postalCode = "97217"
  country = "US"
  
  # Social Links
  socialFacebook = "https://www.facebook.com/10corp"
  socialTwitter = "https://www.twitter.com/10corp"
  socialInstagram = "https://www.instagram.com/10corp"
```

#### Sitemap Configuration
```toml
[sitemap]
  changefreq = "monthly"
  priority = 0.5
  filename = "sitemap.xml"
```

#### Output Formats
```toml
[outputs]
  home = ["HTML", "RSS", "JSON"]
```

---

## 4. Content Frontmatter Format

### Standard Page Template
```yaml
---
title: "Page Title"
seoTitle: "SEO-optimized title for search engines (50-60 chars)"
description: "Meta description for SEO (150-160 characters)"
keywords:
  - "keyword1"
  - "keyword2"
  - "keyword3"
image: "/images/page-image.png"
author: "10Corp"
url: "/custom/path/"  # Optional
robots: "index, follow"  # Optional, defaults to index, follow
builder: true
date: 2024-12-24T00:00:00+00:00
---
```

### Blog Post Template
```yaml
---
title: "Blog Post Title"
seoTitle: "SEO Title for Search Results"
description: "Compelling meta description"
keywords:
  - "topic keyword"
  - "related term"
image: "/images/blog/post-image.png"
author: "Author Name"
date: 2024-12-24T09:00:00+00:00
---
```

---

## 5. Robots.txt Template

### Location: `layouts/robots.txt`

Features:
- Allows all user agents by default
- Auto-disallows pages with `robots: "noindex, nofollow"`
- Excludes admin areas
- Excludes 404 page
- Links to sitemap

---

## 6. SEO Best Practices Implemented

### Technical SEO
✅ Canonical URLs on all pages
✅ Proper hreflang tags for internationalization
✅ Mobile-responsive viewport meta tags
✅ Structured data for rich snippets
✅ XML sitemap generation
✅ Robots.txt for crawler control
✅ Hugo generator tag removed
✅ Absolute URLs for images

### On-Page SEO
✅ Hierarchical title tag structure
✅ Unique meta descriptions per page
✅ Keyword optimization support
✅ Image alt text support
✅ Breadcrumb navigation (schema)
✅ Internal linking structure (menu)

### Social Media Optimization
✅ Complete Open Graph implementation
✅ Twitter Cards with large images
✅ Social profile linking (sameAs)
✅ Image optimization for sharing

### Local SEO
✅ LocalBusiness schema
✅ NAP (Name, Address, Phone) consistency
✅ Geo-coordinates in schema
✅ Business hours specification
✅ Service area specification

---

## 7. Testing & Validation

### Recommended Tools
1. **Google Search Console**: Submit sitemap, monitor indexing
2. **Rich Results Test**: https://search.google.com/test/rich-results
3. **Schema Markup Validator**: https://validator.schema.org/
4. **Open Graph Debugger**: https://developers.facebook.com/tools/debug/
5. **Twitter Card Validator**: https://cards-dev.twitter.com/validator
6. **PageSpeed Insights**: https://pagespeed.web.dev/
7. **Mobile-Friendly Test**: https://search.google.com/test/mobile-friendly

### Testing Checklist
- [ ] Validate all structured data with Schema.org validator
- [ ] Check Open Graph tags with Facebook debugger
- [ ] Verify Twitter Cards display correctly
- [ ] Confirm canonical URLs are absolute
- [ ] Test breadcrumbs appear in search results
- [ ] Verify sitemap.xml is accessible
- [ ] Check robots.txt accessibility
- [ ] Monitor Core Web Vitals

---

## 8. Maintenance Guidelines

### Regular Updates
1. **Pricing Data**: Update service schema prices annually
2. **priceValidUntil**: Extend dates in service schema
3. **Business Hours**: Update if schedule changes
4. **Contact Information**: Keep NAP consistent across all schemas
5. **Social Links**: Add new profiles to config and schema

### Content Creation
- Always include `seoTitle`, `description`, and `keywords`
- Use descriptive, unique titles (50-60 characters)
- Write compelling meta descriptions (150-160 characters)
- Include high-quality images (1200x630px recommended)
- Set proper `date` in ISO 8601 format
- Choose appropriate `robots` directives

### Monitoring
- Weekly: Check Google Search Console for errors
- Monthly: Review organic traffic and keyword rankings
- Quarterly: Audit structured data with validation tools
- Annually: Review and update schema.org types

---

## 9. Advanced Features

### Dynamic Breadcrumbs
Automatically generated from URL structure for all non-homepage pages.

### Conditional Schemas
- BlogPosting schema only appears on blog pages
- WebSite schema only on homepage
- Article tags only on blog posts

### Image Optimization
- All images use absolute URLs (required for social sharing)
- OG images include dimensions for optimal display
- Alt text provided for accessibility and SEO

### Multilingual Support
- Locale specifications for en-US, fr-FR, es-ES
- Hreflang tags for language targeting
- Contact point language specifications

---

## 10. Performance Considerations

### Structured Data Size
Current implementation includes ~5KB of JSON-LD per page. This is well within acceptable limits and provides comprehensive rich snippet support.

### Caching
- Hugo generates static structured data at build time
- No runtime overhead
- All schemas are minified in production

### Load Order
- Critical SEO tags in `<head>`
- Structured data loaded before closing `</head>`
- No render-blocking issues

---

## 11. Future Enhancements

### Potential Additions
- [ ] FAQ schema for service pages
- [ ] Product schema for e-commerce pages
- [ ] Video schema for video content
- [ ] Event schema for webinars/events
- [ ] Review aggregation system
- [ ] AggregateRating with actual customer data
- [ ] HowTo schema for tutorial content

### Analytics Integration
- Enhanced e-commerce tracking
- Event tracking for conversions
- Schema.org PropertyValue for custom dimensions

---

## Contact & Support

For questions about SEO implementation:
- **Email**: info@10corp.com
- **Documentation**: This file
- **Hugo SEO Docs**: https://gohugo.io/templates/internal/#open-graph

---

**Version**: 2.0  
**Build System**: Hugo Static Site Generator  
**Theme**: Terio  
**Production URL**: https://www.10corp.com
