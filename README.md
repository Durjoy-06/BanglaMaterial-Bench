# BanglaMaterial-Bench — Pilot v0.1

এই template-টি বাংলাদেশি material culture নিয়ে একটি ছোট, provenance-aware VLM evaluation dataset তৈরির জন্য।

## শুরু করার নিয়ম

1. প্রথমে `docs/collection_log.csv`-এ সম্ভাব্য ছবির উৎস নথিভুক্ত করুন।
2. অনুমতি ও license যাচাইয়ের আগে কোনো ছবি dataset-এ অন্তর্ভুক্ত করবেন না।
3. গ্রহণ করা ছবির ID দিন: `BMB_DOM_0001`, `BMB_TEX_0001` ইত্যাদি।
4. মূল ছবি অপরিবর্তিতভাবে `data/images/raw/{web|local}/{CATEGORY}/`-এ রাখুন।
5. ছবির metadata `metadata.csv` এবং `metadata.json`—দুই জায়গাতেই রাখুন।
6. প্রশ্ন ও ground truth `annotations/questions/questions.csv`-এ রাখুন।
7. দ্বিতীয় reviewer-এর মতামত `annotations/reviews/review_log.csv`-এ রাখুন।
8. Pilot শেষ হলে image-level ভিত্তিতে train/dev/test split নয়, প্রথমে held-out test split নির্ধারণ করুন। একই মূল ছবি, crop বা near-duplicate যেন একাধিক split-এ না যায়।

## Category IDs

- `DOM`: Traditional domestic tools
- `TEX`: Textiles and weaving
- `ART`: Folk/popular art
- `POT`: Pottery and clay household objects
- `CRA`: Craft and material artifacts

## Image ID format

`BMB_{CATEGORY}_{4-digit-number}`

উদাহরণ: `BMB_DOM_0001`

Question ID format: `{IMAGE_ID}_Q01`

## Provenance ও evidence

- `source_type`: `web` অথবা `local`
- Web ছবির ক্ষেত্রে মূল URL, creator, license name/URL এবং access date লিখুন।
- Local ছবির ক্ষেত্রে photographer/collector code, capture date, consent status ও location granularity লিখুন।
- সাংস্কৃতিক পরিচয় শুধু filename বা search result দেখে নিশ্চিত করবেন না।
- `expert_verified=true` শুধু তখনই দিন যখন উপযুক্ত জ্ঞানসম্পন্ন reviewer সত্যিই যাচাই করেছেন।
- কোনো ছবির license/consent অস্পষ্ট হলে `status=hold` রাখুন; public release-এ দেবেন না।
- ব্যক্তির মুখ, নাম, বাড়ি বা অন্য সংবেদনশীল তথ্য থাকলে privacy ও consent বিবেচনা করুন।

## প্রশ্ন তৈরির নিয়ম

প্রতি ছবিতে 3–5টি প্রশ্ন দিয়ে শুরু করুন:
1. Object identity
2. Visible attributes
3. Function/use (প্রয়োজন হলে external evidence)
4. Parts/spatial relationships
5. Cultural interpretation (শুধু যথেষ্ট প্রমাণ থাকলে)

প্রতিটি প্রশ্নে evidence type লিখুন: `visual`, `external_cultural`, বা `mixed`।
একাধিক গ্রহণযোগ্য উত্তর থাকলে `acceptable_answers`-এ JSON array হিসেবে রাখুন।
মডেলের উত্তর পরে দেখে ground truth বদলাবেন না; ground truth আগে নির্ধারণ ও review করুন।

## গুরুত্বপূর্ণ সতর্কতা

- এই template কোনো dataset-কে নিজে থেকে expert-verified করে না।
- উদাহরণস্বরূপ category/name কেবল প্রাথমিক label; প্রতিটি ছবির জন্য যাচাই প্রয়োজন।
- একই ছবির একাধিক প্রশ্ন independent image sample নয়। ফলাফলে image-level clustering বিবেচনা করুন।
- Benchmark-এ public test answer প্রকাশ করলে ভবিষ্যৎ evaluation contamination হতে পারে; প্রয়োজনে test labels private রাখুন।
