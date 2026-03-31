---
name: arabic-content-creator
description: >
  The definitive Arabic content skill for AI agents. 22 Arab countries, 10+ major dialects,
  platform-by-platform strategy, and deep cultural intelligence. Write Gulf, Egyptian, Levantine,
  Iraqi, Maghrebi, Sudanese, and MSA content that sounds native — not translated. Covers:
  social media (X, Instagram, TikTok, Snapchat, LinkedIn, YouTube), blogs, SEO, email, ads,
  UI/UX, and Arabizi. Includes: dialect grammar rules, country-specific platform preferences,
  religious/cultural sensitivity matrix, hashtag strategy, and RTL technical guidelines.
  Use when writing ANY Arabic content, translating to Arabic, localizing for MENA, or when
  user mentions عربي, بالعربي, خليجي, مصري, شامي, مغربي, عراقي, سوشيال ميديا.
license: MIT
metadata:
  author: ASD-AI
  version: "2.0.0"
  category: content
  tags: [arabic, content-writing, social-media, seo, mena, gulf, egyptian, levantine, iraqi, maghrebi, rtl, localization, copywriting, dialect, marketing]
  platforms: [openclaw, claude-code, gemini-cli, codex-cli, cursor]
  homepage: https://github.com/sanada123/openclaw-skills
---

# Arabic Content Creator v2

**اكتب عربي زي أهل البلد — مش ترجمة آلية.**

Arabic is not one language. It's 22 countries, 10+ dialects, 400+ million speakers, and a
massive gap in AI content tools. This skill turns any AI model into a native-level Arabic
content creator by teaching it what no training data captures: which dialect for which audience,
which platform for which country, which cultural lines never to cross, and how Arabs actually
write online.

## Core Philosophy

```
DIALECT FIRST.     MSA is for news anchors. Real content speaks the audience's dialect.
CULTURE OVER TRANSLATION.  Don't translate American marketing. Adapt Arab values.
PLATFORM × COUNTRY.  Saudi Snapchat ≠ Egyptian TikTok ≠ Lebanese Instagram.
NATURAL > CORRECT.   A "wrong" sentence that sounds human beats a "correct" one that sounds robotic.
RESPECT ALWAYS.     Religion, family, and honor are non-negotiable. When in doubt, don't.
```

---

## When to Activate

- Writing any content in Arabic (any dialect, any platform)
- Translating/localizing content for any Arab country
- Creating Arabic SEO, email, ads, social media, or UI/UX
- User says: عربي, بالعربي, ترجم, محتوى, خليجي, مصري, شامي
- Marketing to MENA audience

## When NOT to Use

- Quran/Hadith quotation (requires Islamic scholarship)
- Legal contracts (requires certified legal translator)
- Medical prescriptions/diagnosis (requires medical Arabic)
- Classical Arabic poetry (specialized literary skill)

---

## 1. The Complete Arabic Dialect Map

### Major Dialect Groups

| Dialect | Countries | Speakers | Mutual Intelligibility |
|---------|-----------|----------|----------------------|
| **Gulf (خليجي)** | KSA, UAE, Kuwait, Qatar, Bahrain, Oman | ~60M | High within Gulf. Medium with Egypt. |
| **Najdi (نجدي)** | Central Saudi (Riyadh) | ~15M | Subtype of Gulf. Distinct vocabulary. |
| **Hejazi (حجازي)** | Western Saudi (Jeddah, Mecca, Medina) | ~10M | More Egyptian influence. |
| **Egyptian (مصري)** | Egypt | ~110M | Understood EVERYWHERE (TV/film influence) |
| **Levantine (شامي)** | Lebanon, Syria, Jordan, Palestine | ~50M | Soft, melodic. French influence in Lebanon. |
| **Iraqi (عراقي)** | Iraq | ~42M | Distinct. Persian/Turkish loanwords. |
| **Yemeni (يمني)** | Yemen | ~30M | Archaic features, unique vocabulary. |
| **Sudanese (سوداني)** | Sudan | ~44M | Distinct. Some Nubian influence. |
| **Moroccan (دارجة)** | Morocco | ~37M | Heavy French/Berber. Least understood elsewhere. |
| **Algerian (دزيرية)** | Algeria | ~44M | French-heavy. Close to Moroccan. |
| **Tunisian (تونسي)** | Tunisia | ~12M | French-Italian influence. |
| **Libyan (ليبي)** | Libya | ~7M | Between Maghrebi and Egyptian. |
| **MSA (فصحى)** | All Arab countries | Written standard | Formal. Nobody speaks it naturally. |

### Sub-Dialects That Matter for Marketing

**Saudi Arabia (biggest ad market in MENA):**

| Sub-dialect | Region | How it sounds | Use for |
|-------------|--------|---------------|---------|
| Najdi | Riyadh, Qassim | "ايش" for what, "وش" for what | National brands, tech |
| Hejazi | Jeddah, Mecca | Softer, "إيه" for yes | Lifestyle, tourism, food |
| Southern | Abha, Jizan | Distinct accent, unique words | Local campaigns only |
| Eastern | Dammam, Khobar | Close to Bahraini/Kuwaiti | Oil sector, B2B |

**UAE:**

| Register | When | Example |
|----------|------|---------|
| Emirati dialect | Local audience | "شحالك" (how are you) |
| Gulf-neutral | Business | "كيف الحال" |
| English-heavy | Dubai expat content | "Check out our latest deal يا جماعة" |

### Dialect Grammar Quick Reference

**Gulf distinguishing features:**
- Future tense: "ب" prefix → "بروح" (I will go)
- Question "what": "وش" or "ايش" (vs MSA "ماذا")
- Negation: "ما" before verb → "ما أبي" (I don't want)
- Feminine "you": "انتي" (standard), "إنتِ"
- Possessive: "حقي" / "حقك" (my/your) — Gulf-specific
- Common filler: "يعني" (like, I mean)

**Egyptian distinguishing features:**
- Future: "ه" prefix → "هروح" (I will go)
- Question "what": "إيه"
- Negation: "مش" → "مش عايز" (I don't want)
- "ج" pronounced as hard "G" → "جمال" = "Gamal"
- Common fillers: "يعني", "بقى", "طب"
- Emphasis: "خالص" (at all), "أوي" (very)

**Levantine distinguishing features:**
- Future: "رح" → "رح أروح" (I will go)
- Question "what": "شو"
- Negation: "ما" or "مو" → "مو هيك" (not like this)
- Lebanese French words: "بونجور", "ميرسي", "Ca va"
- "ق" often dropped → "قلت" becomes "إلت"
- Softer, more melodic intonation

**Iraqi distinguishing features:**
- "چ" for "ك" in some words → "چلب" (dog)
- "گ" sound exists (doesn't in other dialects)
- Question "what": "شنو" or "شكو ماكو" (what's up — uniquely Iraqi)
- Persian loanwords: "جاي" (tea from چای)
- Turkish loanwords: "طابق" (floor), "باجة" (dish)

**Moroccan/Maghrebi distinguishing features:**
- Heavy French integration: "نورمال", "ترانكيل", "بزاف" (beaucoup → a lot)
- Shortened words: "كيداير" (how are you, from كيف الدير)
- Very different from Gulf — **NOT mutually intelligible**
- Numbers often in French: "واحد، زوج، تلاتة" (standard) but "سينكون" (50 from cinquante)
- "ش" negation suffix: "ماعرفتش" (I didn't know)

---

## 2. Country × Platform Matrix

**Which platforms dominate where:**

| Country | #1 Platform | #2 | #3 | Notes |
|---------|------------|-----|-----|-------|
| 🇸🇦 Saudi | X (Twitter) | Snapchat | Instagram | X = king. 79% internet users on X. Snapchat huge for youth. |
| 🇦🇪 UAE | Instagram | LinkedIn | TikTok | Most professional market. LinkedIn big for B2B. |
| 🇪🇬 Egypt | Facebook | TikTok | Instagram | Facebook still #1 (unlike most of world). TikTok exploding. |
| 🇯🇴 Jordan | Facebook | Instagram | TikTok | Facebook dominant. Instagram for youth. |
| 🇱🇧 Lebanon | Instagram | WhatsApp | TikTok | Instagram-first culture. WhatsApp for business. |
| 🇮🇶 Iraq | Facebook | TikTok | Telegram | Facebook massive. Telegram for news/politics. |
| 🇰🇼 Kuwait | Instagram | Snapchat | X | High engagement. Snap for behind-scenes. |
| 🇶🇦 Qatar | Instagram | X | Snapchat | Luxury-focused. High spending audience. |
| 🇧🇭 Bahrain | Instagram | X | Snapchat | Small but high-spending market. |
| 🇴🇲 Oman | Instagram | X | Snapchat | Conservative. Respect in tone. |
| 🇲🇦 Morocco | Facebook | Instagram | TikTok | Darija content. French-Arabic mix. |
| 🇩🇿 Algeria | Facebook | TikTok | YouTube | Darija/French heavy. Facebook dominant. |
| 🇹🇳 Tunisia | Facebook | Instagram | TikTok | Similar to Algeria. French influence. |
| 🇱🇾 Libya | Facebook | TikTok | Telegram | Facebook dominant. Telegram for groups. |
| 🇸🇩 Sudan | Facebook | WhatsApp | TikTok | WhatsApp critical for business. |
| 🇾🇪 Yemen | WhatsApp | Facebook | TikTok | WhatsApp = primary channel. |

### Saudi Arabia Deep Dive (Largest MENA Ad Market)

Saudi is the #1 market. Special rules:

**X/Twitter (79% penetration — highest in the world):**
- Saudis use X like Americans use Instagram — it's THE platform
- Gulf dialect, not MSA
- حسابات موثقة (verified accounts) carry massive weight
- Trend hijacking works — #ترند_السعودية
- Best posting times: 9-11 PM (after Isha prayer), Thursday evening, Friday morning
- During Ramadan: engagement spikes between Iftar (sunset) and Suhoor (pre-dawn)

**Snapchat (Saudi is #1 Snapchat market globally per capita):**
- Behind-the-scenes, raw, unpolished
- Snap Maps for local businesses
- Geofilters for events/stores
- Stories > individual snaps
- Youth-dominated (18-34)

### Egypt Deep Dive (Largest Arab Population)

**Facebook (still king — 42M+ users):**
- Groups > Pages for engagement
- Facebook Marketplace massive for e-commerce
- Video content outperforms everything else
- Egyptian dialect ONLY (MSA = zero engagement)
- Humor is EVERYTHING — Egyptians share funny content

**TikTok (exploding):**
- Egyptian TikTok = comedy + music + social commentary
- Fastest-growing platform in Egypt
- Dialect: pure Egyptian, no MSA
- Duets and reactions drive virality

---

## 3. Content by Type

### Social Media Posts

**Hook Formulas by Dialect:**

| Dialect | Hook | Translation |
|---------|------|-------------|
| Gulf | "أكبر غلطة يسوونها الناس في [topic]:" | "The biggest mistake people make in [topic]:" |
| Gulf | "ليش [thing]? خلني أقولك:" | "Why [thing]? Let me tell you:" |
| Egyptian | "الحاجة اللي محدش بيقولهالك عن [topic]:" | "The thing nobody tells you about [topic]:" |
| Egyptian | "جربت [thing] لمدة [time]. النتيجة صدمتني:" | "I tried [thing] for [time]. The result shocked me:" |
| Levantine | "شو رأيكم بهالشي:" | "What do you think about this:" |
| Levantine | "حكيلكم قصة [topic]:" | "Let me tell you a story about [topic]:" |
| Iraqi | "شگد مهم [topic] — خلوني أشرحلكم:" | "How important [topic] is — let me explain:" |
| Moroccan | "واش عرفتو [thing]? ديرو هاد الحاجة:" | "Did you know [thing]? Do this:" |

**CTA Formulas by Dialect:**

| Dialect | CTA |
|---------|-----|
| Gulf | "سو save لهالبوست 📌" / "شاركه مع شخص يحتاجه" |
| Egyptian | "سيڤ البوست ده 📌" / "ابعته لحد محتاجه" |
| Levantine | "احفظ هالبوست 📌" / "شاركه مع حدا بيحتاجه" |
| Iraqi | "احفظ هالبوست 📌" / "شاركه ويه شخص يحتاجه" |
| Moroccan | "حفظ هاد البوست 📌" / "سيفطيه لشي واحد محتاجه" |

### Blog & SEO

**Arabic SEO — The Untapped Goldmine:**

| Metric | English | Arabic |
|--------|---------|--------|
| Keyword competition | Very high | **Low to medium** |
| Quality content available | Saturated | **Massive gaps** |
| Featured snippet opportunity | Competitive | **Wide open** |
| Voice search growth | Mature | **Explosive growth** |
| Cost per click (ads) | $1-5+ | **$0.10-0.50** |

**Arabic Keyword Research Protocol:**

For any topic, generate ALL of these:
```
1. MSA formal: "التسويق الرقمي"
2. MSA informal: "تسويق رقمي"
3. Dialect (Gulf): "تسويق ديجيتال"
4. Franglais (Maghreb): "ماركوتينغ ديجيتال"
5. English-Arabic mix: "digital marketing بالعربي"
6. Question (MSA): "ما هو التسويق الرقمي"
7. Question (dialect): "ايش التسويق الرقمي" / "يعني ايه تسويق رقمي"
8. Long-tail: "أفضل استراتيجيات التسويق الرقمي للمبتدئين"
9. Arabizi: "el taswe2 el ra2ami" (for youth searches)
10. Voice search: "كيف أسوي تسويق رقمي لمشروعي الصغير"
```

**Blog Template (Arabic SEO):**

```markdown
# [عنوان رئيسي — 50-60 حرف، يحتوي الكلمة المفتاحية]

**وصف ميتا:** [120-155 حرف، كلمة مفتاحية + فائدة + CTA]

## مقدمة (100-150 كلمة)
- ابدأ بالمشكلة (بلهجة القارئ إذا ممكن)
- ماذا سيتعلم
- الكلمة المفتاحية في أول 100 كلمة

## [H2 بالكلمة المفتاحية الثانوية]
- نقاط مختصرة
- أمثلة من السوق العربي (ليس أمثلة أمريكية مترجمة!)
- أرقام محلية

## [H2]
[محتوى]

## [H2 — خطوات عملية]
1. خطوة أولى
2. خطوة ثانية
3. ...

## الخلاصة
- ٣ نقاط رئيسية
- CTA واضح

## الأسئلة الشائعة (FAQ Schema — لـ Google)
**س: [سؤال بالكلمة المفتاحية — بصيغة ما يبحثه الناس فعلاً]**
ج: [2-3 جمل مباشرة]
```

### Email Marketing (Arabic)

**Subject Lines by Market:**

| Market | Style | Example |
|--------|-------|---------|
| Gulf B2B | Respectful + value | "٥ حلول تقنية توفر عليكم ٣٠٪ من التكاليف" |
| Gulf B2C | Offer-driven | "حصرياً — خصم ٤٠٪ لمدة ٤٨ ساعة ⏰" |
| Egyptian | Emotional/funny | "مش هتصدق اللي حصل لما جربنا الأداة دي 😱" |
| Levantine | Personal | "هيدا الإيميل إلك خصيصاً 💌" |
| Moroccan | French-Arabic mix | "Découvrez — اكتشف العرض ديالنا الجديد" |

**Greeting by Market:**

| Market | Formal | Casual |
|--------|--------|--------|
| Gulf | السلام عليكم ورحمة الله | هلا والله |
| Egyptian | السلام عليكم | أهلاً |
| Levantine | مرحبا | هلا / كيفك |
| Iraqi | السلام عليكم | هلا بيك |
| Moroccan | السلام عليكم | أهلا / Salut |

### Ad Copy

**Google Ads (Arabic) — Per Market:**

Saudi example:
```
العنوان: نظام AI لإدارة مشروعك — جاهز خلال ٣٠ دقيقة
الوصف: ١٠ وكلاء ذكاء اصطناعي على تيليجرام. أتمتة كاملة. جربه مجاناً — ضمان استرداد ٣٠ يوم.
```

Egyptian example:
```
العنوان: عايز تكبّر بزنسك؟ AI يشتغلك ٢٤ ساعة
الوصف: ١٠ أدوات ذكاء اصطناعي تشتغل وأنت نايم. ابدأ النهاردة — مجاناً لمدة ١٤ يوم.
```

### UI/UX Copy (Arabic)

| English | ❌ Bad (literal) | ✅ Gulf | ✅ Egyptian | ✅ MSA (default) |
|---------|-----------------|--------|-----------|----------------|
| Sign up | سجّل | سجّل حسابك | سجّل عندنا | أنشئ حساب |
| Log in | دخول | ادخل | سجّل دخولك | تسجيل الدخول |
| Get started | ابدأ | يلا نبدأ | يلا ابدأ | ابدأ الآن |
| Buy now | اشتر الآن | اطلبه الحين | اشتريه دلوقتي | اطلب الآن |
| Loading | جاري التحميل | لحظة... | ثانية واحدة... | جارٍ التحميل... |
| Error | خطأ | عذراً، صار خطأ | في مشكلة حصلت | حدث خطأ |
| Success | نجاح | تم بنجاح 🎉 | تمام! | تمت العملية بنجاح |
| No results | لا نتائج | ما لقينا شيء | مفيش نتايج | لا توجد نتائج |
| Are you sure? | هل أنت متأكد؟ | متأكد؟ | متأكد؟ | هل أنت متأكد؟ |
| Share | شارك | شاركه | شيره | مشاركة |

---

## 4. Cultural Intelligence Matrix

### Religious Sensitivity

| Topic | Rule | Why |
|-------|------|-----|
| **Ramadan** | Content tone shifts to spiritual. Sales OK but respectful. | Holiest month. Aggressive selling = backlash. |
| **Friday** | Reduce posting during Jumu'ah prayer (12-2 PM local). | Disrespectful to compete with prayer time. |
| **Alcohol** | Never mention in Gulf content. OK in Lebanon/Tunisia. | Haram + illegal in most Gulf states. |
| **Pork** | Never mention anywhere. | Universally avoided. Even secular Arabs avoid it in content. |
| **Gender mixing** | Conservative in Saudi/Gulf imagery. Liberal in Lebanon. | Saudi: separate gender imagery. Lebanon: mixed OK. |
| **Music** | Debate in conservative circles. Use nasheed or neutral audio. | Some audiences object to music in content. |
| **Dogs** | Avoid as positive image in Gulf. OK in Maghreb. | Culturally sensitive in Gulf/Mashreq. |
| **Hand gestures** | 👍 OK in most places. Pointing with finger = rude. | Culture-specific gestures can offend. |

### Ramadan Content Strategy

```
Pre-Ramadan (2 weeks before):
- Preparation content
- "Get ready for Ramadan" lists
- Product positioning for the month

Ramadan (30 days):
- Spiritual/inspirational tone
- Post between Iftar and Suhoor (peak engagement)
- Reduce hard-selling, increase value content
- Community-focused campaigns
- Charity/CSR content performs exceptionally well

Eid al-Fitr (end of Ramadan):
- Celebration content
- Gift-giving campaigns
- "Eid Mubarak" messages to audience
- SALE season (like Black Friday in MENA)
```

### National Days & Events Calendar

| Event | Country | Date | Content Opportunity |
|-------|---------|------|-------------------|
| Saudi National Day | KSA | Sep 23 | 🇸🇦 Biggest content day. Green everywhere. |
| UAE National Day | UAE | Dec 2 | 🇦🇪 Patriotic content. |
| Egypt Revolution Day | Egypt | Jul 23 | 🇪🇬 Patriotic + nostalgia |
| Kuwait National Day | Kuwait | Feb 25 | 🇰🇼 Liberation Day Feb 26 also |
| Morocco Throne Day | Morocco | Jul 30 | 🇲🇦 Royal celebration |
| Eid al-Fitr | All | Variable | 🎉 Post-Ramadan celebration |
| Eid al-Adha | All | Variable | 🐑 Sacrifice & family |
| White Friday | MENA | Nov | 🛍️ MENA's Black Friday |

### Humor & Tone by Country

| Country | Humor Style | Tone | Example |
|---------|------------|------|---------|
| 🇸🇦 Saudi | Dry wit, sarcasm | Confident | "ما يحتاج أقولك — أنت تعرف 😏" |
| 🇪🇬 Egypt | Comedy gold, wordplay, absurdist | Warm, loud | "إيه ده يا جدعان 😂😂" |
| 🇱🇧 Lebanon | Sophisticated, French-influenced | Glamorous | "C'est la vie — هيك الدنيا" |
| 🇯🇴 Jordan | Understated, deadpan | Chill | "يا زلمة... عادي" |
| 🇮🇶 Iraq | Direct, dark humor | Resilient | "شكو ماكو — الحياة مستمرة" |
| 🇲🇦 Morocco | Physical comedy, mimicry | Animated | "واش نتا كتهضر بصح؟ 🤣" |

---

## 5. Arabizi (عربيزي) — The Youth Code

Many young Arabs type in Latin characters with numbers replacing Arabic sounds:

| Number | Arabic Sound | Example |
|--------|-------------|---------|
| 2 | ء (hamza) | so2al = سؤال |
| 3 | ع (ain) | 3arabi = عربي |
| 5 | خ (kha) | 5alas = خلاص |
| 6 | ط (ta emphatic) | 6abee3i = طبيعي |
| 7 | ح (ha) | 7abibi = حبيبي |
| 8 | ق (qaf) | 8alb = قلب |
| 9 | ص (sad) | 9a7 = صح |

**When to use Arabizi:**
- TikTok comments
- Informal social media (never in formal content)
- Youth-targeted campaigns (18-25)
- When you want to seem casual/cool

**When NOT to use:**
- SEO content (Google doesn't index Arabizi well)
- Professional/B2B
- Email marketing
- Ad copy
- Audience over 35

---

## 6. Technical RTL Guidelines

### CSS/HTML

```css
/* Root direction */
html[lang="ar"] { direction: rtl; }

/* Font stack for Arabic */
font-family: 'IBM Plex Sans Arabic', 'Noto Sans Arabic', 'Segoe UI', Tahoma, sans-serif;

/* Logical properties (modern CSS — preferred) */
margin-inline-start: 16px;  /* not margin-left */
padding-inline-end: 16px;   /* not padding-right */
border-inline-start: 2px solid; /* not border-left */

/* Flexbox automatically reverses in RTL */
display: flex; /* row direction flips */

/* Icons that need flipping */
.icon-arrow, .icon-back, .icon-forward, .icon-progress {
  transform: scaleX(-1);
}

/* Icons that should NOT flip */
.icon-phone, .icon-clock, .icon-check, .icon-heart {
  /* Don't flip — universally directional */
}
```

### Numbers in Arabic Context

```
/* Numbers are ALWAYS LTR, even inside RTL text */
<span dir="ltr">+966 50 123 4567</span>
<span dir="ltr">$49.99</span>
<span dir="ltr">2026-03-31</span>

/* But Arabic numeral names are RTL */
خمسة وعشرون (twenty-five)
```

### Mixed Language Text

```html
<!-- For mixed Arabic-English paragraphs -->
<p dir="auto">هذا النص يحتوي على English words وكلمات عربية</p>

<!-- For explicit control -->
<bdi>Product Name</bdi> — <span dir="rtl">وصف المنتج بالعربي</span>
```

---

## 7. Hashtag Strategy by Platform & Country

### Saudi X (Twitter)

```
Trending: #السعودية #رؤية_السعودية_2030 #الرياض #جدة
Business: #ريادة_أعمال #تقنية #ذكاء_اصطناعي #تسويق_رقمي
Lifestyle: #سفر #طبخ #رياضة #صحة
Use 3-5 hashtags max on X
```

### Egyptian Facebook/Instagram

```
Trending: #مصر #القاهرة #الاسكندرية
Business: #بيزنس #تسويق #ريادة_أعمال #مشروعات_صغيرة
Lifestyle: #أكل #سفر #موضة
Use 15-20 hashtags on Instagram, 3-5 on Facebook
```

### UAE Instagram

```
Trending: #دبي #أبوظبي #الإمارات
Business: #أعمال #تجارة_إلكترونية #ستارت_اب
Luxury: #فخامة #لايف_ستايل #سيارات
Use 20-25 hashtags, mix Arabic + English
```

---

## 8. Common Mistakes Matrix

| Mistake | Severity | Why | Fix |
|---------|----------|-----|-----|
| Using تشكيل (diacritics) on social media | Medium | Looks academic, not human | Remove all diacritics |
| MSA on TikTok/Snapchat | High | Sounds like a news anchor | Use local dialect |
| Egyptian dialect for Saudi audience | High | Cultural disconnect | Match dialect to audience country |
| Saudi dialect for Egyptian audience | High | Won't understand Gulf words | Use Egyptian or MSA |
| Moroccan dialect for Gulf audience | Critical | Almost unintelligible | Use MSA or Egyptian |
| Translating English idioms literally | Medium | Some work, many don't | Find Arabic cultural equivalent |
| English-only hashtags | Medium | Arabs search in Arabic | Mix Arabic + English hashtags |
| Ignoring gender in copy | Medium | Arabic is gendered language | Use masculine default or address both |
| ي vs ى confusion | Low (but marks non-native) | Spelling convention | ى at end of word, ي in middle |
| ة vs ه confusion | Medium | Changes meaning | تاء مربوطة ة for feminine nouns |
| Posting during Friday prayer | High | Culturally disrespectful | Avoid 12-2 PM Friday |
| Alcohol references in Gulf content | Critical | Illegal + deeply offensive | Never. Zero tolerance. |
| Using 🐷 emoji | Critical | Pork reference | Never in any Arab content |
| Left-to-right layout for Arabic | Critical | Unusable | Always RTL |
| Long paragraphs | Medium | Arabs scan on mobile like everyone | 1-2 lines max per paragraph |

---

## Output Standards

When creating Arabic content:
1. **State dialect + country** before writing: "Gulf dialect, Saudi audience"
2. **Never mix dialects** in one piece — pick one, commit
3. **RTL formatting** — all output right-to-left
4. **No diacritics** on social/digital content
5. **Culture check** — religion, gender, dietary, holiday awareness
6. **Platform match** — right platform for right country
7. **Proofread for** — ي vs ى, ة vs ه, همزة, spacing after ال
8. **Arabizi** — only when targeting youth in casual context
9. **Time zones** — MENA spans UTC+0 (Morocco) to UTC+4 (UAE). Schedule accordingly.
10. **Adapt, don't translate** — cultural adaptation > literal translation

---

*لأن ٤٠٠ مليون عربي يستحقون محتوى يتكلم لغتهم الحقيقية — مش لغة Google Translate.*

**Contributing:** Native speakers of any Arabic dialect — your corrections and additions are welcome. 
Open an issue or PR at [github.com/sanada123/openclaw-skills](https://github.com/sanada123/openclaw-skills).
