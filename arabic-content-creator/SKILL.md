---
name: arabic-content-creator
description: >
  Write native Arabic content that sounds human, not translated. Gulf dialect for social media,
  MSA for formal content, Egyptian for viral reach. Covers: social media posts, blog articles,
  email campaigns, ad copy, product descriptions, SEO content, and UI/UX copy — all in Arabic
  with proper RTL formatting. Use when writing any Arabic content, translating to Arabic,
  localizing products for MENA, creating Arabic social media posts, writing Arabic emails,
  Arabic SEO, or when user mentions عربي, بالعربي, ترجم, محتوى عربي, سوشيال ميديا.
  Triggers on: Arabic, عربي, Gulf, خليجي, MENA, translate to Arabic, RTL content.
license: MIT
metadata:
  author: ASD-AI
  version: "1.0.0"
  category: content
  tags: [arabic, content-writing, social-media, seo, mena, gulf, rtl, localization, copywriting, translation]
  platforms: [openclaw, claude-code, gemini-cli, codex-cli, cursor]
  homepage: https://github.com/sanada123/openclaw-skills
---

# Arabic Content Creator

**اكتب عربي كأنك عربي — مش ترجمة Google.**

Most AI-generated Arabic reads like bad machine translation. Stiff MSA where Gulf slang belongs.
Egyptian dialect in a Saudi ad. Formal tone in a TikTok caption. This skill fixes that by
teaching the model how Arabs actually write online — which dialect for which platform, which
tone for which audience, and which mistakes to never make.

## Core Philosophy

```
DIALECT > MSA for social media. Always.
NATURAL > CORRECT. A grammatically "wrong" post that sounds human beats a perfect one that sounds robotic.
CULTURE > TRANSLATION. Don't translate concepts. Adapt them.
CONTEXT > RULES. Saudi Twitter ≠ Egyptian Instagram ≠ UAE LinkedIn.
```

---

## When to Activate

- Writing any content in Arabic (social, blog, email, ads, product, UI)
- Translating English content to Arabic
- Localizing a product/website for MENA market
- Creating Arabic SEO content
- Writing Arabic UI/UX copy (buttons, errors, onboarding)
- User says: عربي, بالعربي, ترجم, محتوى, سوشيال ميديا

## When NOT to Use

- Legal/medical/religious content (requires certified specialist)
- Classical Arabic poetry or Quranic text (requires specialized knowledge)
- Formal government correspondence (use dedicated legal skill)

---

## 1. Arabic Dialect Map

**The #1 mistake: using the wrong dialect.** Arabic is not one language — it's a family.

| Dialect | Where | Use For | Sounds Like |
|---------|-------|---------|-------------|
| **Gulf (خليجي)** | KSA, UAE, Kuwait, Qatar, Bahrain, Oman | Business, luxury, fintech, real estate | Formal but warm. "حياكم" not "أهلاً" |
| **Egyptian (مصري)** | Egypt + understood everywhere | Entertainment, viral content, comedy | Casual, expressive. "إيه ده" not "ما هذا" |
| **Levantine (شامي)** | Lebanon, Syria, Jordan, Palestine | Lifestyle, food, travel | Soft, melodic. "كيفك" not "كيف حالك" |
| **MSA (فصحى)** | Formal writing everywhere | Blogs, press, corporate, SEO | News anchor tone. Grammatically precise. |
| **North African (مغاربي)** | Morocco, Algeria, Tunisia | Local markets only | French-influenced. Least understood elsewhere. |

### Decision Matrix: Which Dialect to Use

| Content Type | Saudi Audience | Pan-Arab | Egyptian Market |
|-------------|---------------|----------|----------------|
| Social media | Gulf | Egyptian (widest reach) | Egyptian |
| Blog/SEO | MSA | MSA | MSA |
| Email marketing | Gulf or MSA | MSA | Egyptian or MSA |
| Ad copy | Gulf | Egyptian | Egyptian |
| Product UI | MSA | MSA | MSA |
| Customer support | Gulf | MSA | Egyptian |
| LinkedIn | MSA | MSA | MSA |
| TikTok/Reels | Gulf slang | Egyptian | Egyptian |

---

## 2. Social Media — Platform by Platform

### Twitter/X (Saudi = largest Arab market on X)

**Format:**
```
[Hook — 1 line, punchy, Gulf dialect]

[Body — 2-3 short lines, spaced]

[CTA or question]

#هاشتاق_عربي #الهاشتاق_بالعربي
```

**Hook formulas (Gulf):**
- "أكبر غلطة يسوونها الناس في [topic]:"
- "ليش [counterintuitive thing]? خلني أقولك:"
- "جربت [thing] لمدة [time]. النتيجة:"
- "٣ أشياء تمنيت أعرفها قبل [experience]:"
- "الفرق بين [A] و [B] بجملة وحدة:"

**Rules:**
- Hashtags in Arabic (not English)
- No تشكيل (diacritics) on social media — looks pretentious
- Use numbers in Arabic numerals (٣ ،٢ ،١) or Western (1, 2, 3) — both accepted
- Keep under 200 characters for maximum engagement
- Emojis: use sparingly. Gulf audience prefers clean text.

### Instagram

**Captions (Gulf/Egyptian based on audience):**
```
[Strong first line — the preview before "more"]

[Story or value — 3-5 short paragraphs]

[CTA: "سو save لهالبوست 📌" or "شاركه مع شخص يحتاجه"]

.
.
.
[Hashtags — 15-20, mix of Arabic + English for reach]
```

**Hashtag strategy:**
- 5 broad: #ريادة_أعمال #تسويق_رقمي #بزنس #محتوى #نجاح
- 5 medium: #تسويق_سعودي #ستارت_اب #رواد_اعمال_العرب
- 5 niche: #[specific topic hashtags]
- 5 English: #startup #marketing #business (for discoverability)

### TikTok / Reels

**Script structure:**
```
ثانية 1-3: Hook (وقف السكرول)
"الشيء اللي ما يقولونه لك عن [topic]..."

ثانية 4-15: Content (القيمة)
[3 نقاط سريعة، كل وحدة بجملة]

ثانية 16-20: CTA
"فولو عشان المزيد 👆"
```

**Gulf TikTok rules:**
- Speak Gulf dialect, NOT MSA (sounds like a textbook)
- Fast pace — Arabs scroll faster than global average
- Text overlays in Arabic (bold, large, RTL)
- Trending sounds work — but local trends > global trends

### LinkedIn (Arabic)

**Always MSA.** LinkedIn Arabic = professional. No dialect.

```
[Hook — 1 line, professional but not boring]

[Story from experience — 3-4 paragraphs]

[Key takeaway — bold or numbered]

[Question to invite discussion]

#قيادة #إدارة #ريادة_أعمال #تقنية
```

---

## 3. Blog & SEO Content (Arabic)

### Arabic SEO Fundamentals

**Critical differences from English SEO:**

| Factor | English | Arabic |
|--------|---------|--------|
| **Keywords** | Single form | Must target multiple word forms (مفرد، جمع، مصدر) |
| **Search behavior** | Specific queries | Arabs search in dialect + MSA (target both) |
| **Featured snippets** | Well-established | Growing — opportunity to dominate |
| **Competition** | High | Low-medium (massive opportunity in most niches) |
| **Content length** | 1500-2000 words | 1000-1500 sufficient (less competition) |

### Keyword Research (Arabic)

```
For any English keyword, generate:
1. MSA equivalent: "التسويق الرقمي"
2. Dialect variants: "تسويق ديجيتال" / "ماركتنج"
3. Question forms: "كيف أبدأ التسويق الرقمي" / "ايش التسويق الرقمي"
4. Long-tail: "أفضل استراتيجيات التسويق الرقمي للمبتدئين ٢٠٢٦"
```

### Blog Post Template (Arabic SEO)

```markdown
# [عنوان رئيسي يحتوي الكلمة المفتاحية — 50-60 حرف]

**وصف ميتا:** [جملة واحدة تلخص المقال وتحتوي الكلمة المفتاحية — 120-155 حرف]

## مقدمة (100-150 كلمة)
- ابدأ بمشكلة يعاني منها القارئ
- اذكر ما سيتعلمه في المقال
- استخدم الكلمة المفتاحية في أول 100 كلمة

## [عنوان فرعي H2 بالكلمة المفتاحية الثانوية]
- نقاط واضحة ومختصرة
- أمثلة حقيقية من السوق العربي (مش أمثلة أمريكية مترجمة)
- أرقام وإحصائيات عربية عندما يكون ممكن

## [عنوان فرعي H2]
[محتوى]

## الخلاصة
- ٣ نقاط رئيسية
- CTA واضح
- سؤال يشجع التعليقات

## الأسئلة الشائعة (FAQ — لـ AEO)
**س: [سؤال شائع بالكلمة المفتاحية]**
ج: [إجابة مختصرة في 2-3 جمل]
```

---

## 4. Email Marketing (Arabic)

### Subject Line Formulas

| Formula | Example |
|---------|---------|
| **العدد + الفائدة** | "٥ أدوات AI تختصر عليك ٣ ساعات يومياً" |
| **السؤال** | "هل تعرف الغلطة اللي تكلفك عملاء كل يوم؟" |
| **الإلحاح** | "آخر يوم — العرض ينتهي الليلة" |
| **الفضول** | "الشيء اللي غيّر شغلي بالكامل..." |
| **الشخصي** | "{الاسم}، عندك ٣ دقايق؟" |

### Email Body (Gulf B2B)

```
السلام عليكم {الاسم}،

[جملة واحدة تربطك بالقارئ]

[المشكلة — 2-3 جمل]

[الحل — ما تقدمه]

[دليل — رقم أو شهادة عميل]

[CTA واضح — زر واحد]

مع التحية،
[الاسم]
```

**Rules:**
- Always start with السلام عليكم (not مرحبا) for Gulf B2B
- Keep paragraphs 1-2 lines max
- One CTA only
- Sender name in Arabic
- Unsubscribe link mandatory (Arabic text: "إلغاء الاشتراك")

---

## 5. Ad Copy (Arabic)

### Google Ads (Arabic)

```
العنوان 1 (30 حرف): [كلمة مفتاحية + فائدة]
العنوان 2 (30 حرف): [عرض أو ميزة فريدة]
العنوان 3 (30 حرف): [CTA]
الوصف (90 حرف): [توسيع + إلحاح + CTA]
```

**Example:**
```
العنوان 1: نظام AI لإدارة فريقك
العنوان 2: جاهز خلال ٣٠ دقيقة | بدون برمجة
العنوان 3: جربه مجاناً الحين
الوصف: ١٠ وكلاء AI على تيليجرام. ذاكرة دائمة وأتمتة كاملة. ابدأ اليوم — ضمان استرداد ٣٠ يوم.
```

### Meta/Facebook Ads (Arabic)

**Primary text (Gulf):**
```
[Hook — سطر واحد يوقف السكرول]

[المشكلة بـ 2 سطر]

[الحل بـ 2 سطر]

[Social proof — رقم أو شهادة]

[CTA] 👇
```

---

## 6. UI/UX Copy (Arabic)

### Common Patterns

| English | ❌ Bad Arabic | ✅ Good Arabic |
|---------|-------------|--------------|
| Sign up | سجّل | أنشئ حساب |
| Log in | تسجيل الدخول | دخول |
| Get started | ابدأ | ابدأ الآن |
| Learn more | تعلم المزيد | اعرف أكثر |
| Buy now | اشتر الآن | احصل عليه الآن |
| Free trial | تجربة مجانية | جرّبه مجاناً |
| Contact us | اتصل بنا | تواصل معنا |
| Go back | عد | رجوع |
| Error occurred | حدث خطأ | عذراً، حصل خطأ |
| Loading | جاري التحميل | لحظة... |

### RTL Design Rules

- Entire layout flips (navigation, cards, icons)
- Icons with direction (arrows, progress) must flip
- Numbers stay LTR inside RTL text
- Phone numbers: always LTR
- Mixed Arabic-English: use `dir="auto"` on containers
- Don't just `text-align: right` — use `direction: rtl` on the root

---

## 7. Common Mistakes (Never Do These)

| Mistake | Why It's Bad | Fix |
|---------|------------|-----|
| Using تشكيل on social media | Looks academic, not human | Drop all diacritics |
| MSA on TikTok | Sounds like a news anchor | Use dialect |
| Egyptian dialect for Saudi audience | Cultural mismatch | Match dialect to audience |
| Translating English idioms literally | "كسر الجليد" works, "ضرب المسمار على الرأس" doesn't | Adapt, don't translate |
| English hashtags only | Arabs search in Arabic | Mix Arabic + English hashtags |
| Ignoring gender in CTA | Arabic is gendered | Use masculine default or neutral phrasing |
| Using ي instead of ى (and vice versa) | Marks you as non-native | ى at end of word, ي in middle |
| Long paragraphs | Arabs scan, don't read walls of text | 1-2 lines per paragraph max |

---

## Output Standards

When creating Arabic content:
- **State the dialect** before writing: "Using Gulf dialect for Saudi X audience"
- **Never mix dialects** in one piece — pick one and commit
- **RTL formatting**: Ensure all output is properly right-to-left
- **No diacritics** on social media content
- **Culture check**: Avoid alcohol, gambling, pork references in Gulf content
- **Gender awareness**: Arabic is gendered — default masculine or use neutral forms
- **Proofread for**: ي vs ى, ة vs ه, همزة placement, تاء مربوطة

---

*Because 400 million Arabic speakers deserve content that sounds like them, not Google Translate.*
