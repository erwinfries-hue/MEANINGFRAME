# MEANINGFRAME — UX, USER FLOWS & CORE COPY

## 1. Experience principles

1. Start with the person, not the technology.
2. Ask one emotionally simple question at a time.
3. Show why a question matters.
4. Make optional depth clearly optional.
5. Reflect understanding before generating art.
6. Never surprise the customer with a paywall before showing value.
7. Use art language, not model or prompt language.
8. Keep private data private by default.
9. Make every wait state honest and useful.
10. Keep the mobile experience first-class.

## 2. Primary customer flow

### Flow 0 — Landing

The visitor must understand within ten seconds:

- this creates personal art about someone meaningful;
- the process is guided;
- a personal preview is free;
- physical and digital editions exist;
- private photos are not used for training.

Primary CTA: `Kunstwerk beginnen` / `Begin an artwork`

Secondary CTA: `Beispiel ansehen` / `View an example`

### Flow 1 — Project start

Screen 1:

> Für wen entsteht dieses Kunstwerk?

Options:

- Für einen besonderen Menschen
- Für uns als Paar oder Familie
- Für mich selbst

MVP default and marketing path: `Für einen besonderen Menschen`.

Screen 2:

> Was möchtest du mit dem Kunstwerk ausdrücken?

Options:

- Einen bedeutenden Geburtstag feiern
- Ein Lebenswerk würdigen
- Unsere gemeinsame Geschichte zeigen
- Danke sagen
- Etwas anderes

Screen 3:

Collect Co-Author email with clear purpose:

> Wohin dürfen wir deinen Entwurf sichern?

Starting the session may occur before verification. Free preview generation requires a verified email magic link.

### Flow 2 — Co-Author Session

Target completion time: 6–9 minutes.

Use a calm progress indicator with meaningful stages, not a percentage fabricated from variable branching:

1. Beziehung
2. Persönlichkeit
3. Erinnerungen
4. Bildsprache
5. Bestätigung

#### Stage A — Relationship

Required:

- subject display name or nickname;
- relationship to Co-Author;
- selected occasion;
- pronoun form or neutral language choice;
- whether the subject is an adult.

Example:

> Wenn du diese Person jemandem in einem Satz vorstellen würdest – was würdest du sagen?

#### Stage B — Identity

Required:

- select up to five trait chips;
- describe one trait with a concrete example;
- select core emotional impression.

Suggested traits:

- warmherzig
- mutig
- ruhig
- humorvoll
- verlässlich
- freiheitsliebend
- neugierig
- kreativ
- grosszügig
- beharrlich
- verbindend
- weise

The list must be localised and allow custom text.

Example follow-up:

> Du hast „verlässlich“ gewählt. Gibt es einen kleinen Moment, der genau das zeigt?

#### Stage C — Life and memory

Ask adaptively:

- one meaningful life chapter;
- one shared memory;
- important places;
- passions or recurring objects;
- people or relationships that may be symbolically represented;
- one thing that should never be omitted.

Do not require exact dates.

#### Stage D — Emotional and visual direction

Ask:

- what should the recipient feel on seeing it?
- which colour family feels right?
- which symbols feel authentic?
- what must not appear?
- select one Art World after seeing representative non-customer examples.

Emotional intentions:

- gesehen
- gewürdigt
- geliebt
- stolz
- verbunden
- inspiriert
- dankbar
- ruhig

#### Stage E — Photos

Copy:

> Fotos helfen uns, die Person wiedererkennbar darzustellen. Zwei bis fünf unterschiedliche, gut erkennbare Bilder sind ideal.

Photo guidance:

- face visible;
- recent or representative;
- different angles helpful;
- avoid heavy filters;
- at least one single-person photo;
- uploads optional, but warn that recognisable likeness cannot be promised without them.

Consent checkbox:

> Ich darf diese Fotos für die Erstellung des privaten Kunstwerks verwenden.

Never pre-check consent.

### Adaptive-question rules

Claude may ask no more than three dynamic follow-up questions.

A follow-up is justified only when:

- a selected trait has no evidence or example;
- two inputs conflict materially;
- the requested symbol could be interpreted in incompatible ways;
- the emotional intent is unclear;
- the information is insufficient for the selected Art World.

Claude must not:

- diagnose personality;
- infer sensitive traits;
- ask for unnecessary health, political, religious or sexual information;
- force disclosure;
- repeat a question already answered.

### Flow 3 — Meaning Map

The Meaning Map view shows:

- `Essence`: 2–3 sentence human summary;
- `What defines them`: 3–5 traits with supporting moments;
- `Life anchors`: places, chapters and relationships;
- `Visual symbols`: selected symbols and their confirmed meaning;
- `Emotional direction`;
- `Colour atmosphere`;
- `Must include`;
- `Must avoid`.

Every section can be edited.

Confirmation copy:

> Ist das die Person, die du vor Augen hast?

Actions:

- `Ja, das trifft es`
- `Etwas anpassen`

Once confirmed, create an immutable version used for the preview. Later edits create a new version.

### Flow 4 — Art World selection

Show the three Art Worlds with representative sample art and a one-sentence fit recommendation.

Claude may recommend one based on the Meaning Map, but must explain:

> Poetic Symbolism passt besonders gut, weil Erinnerungen, Wärme und persönliche Symbole im Mittelpunkt stehen.

The Co-Author remains free to choose.

### Flow 5 — Personal Preview

Preconditions:

- email verified;
- Meaning Map confirmed;
- Art World selected;
- required consent recorded;
- rate limits passed.

Wait-state sequence:

1. `Wir übersetzen deine Meaning Map in eine Bildidee.`
2. `Komposition und Symbole werden aufeinander abgestimmt.`
3. `Deine persönliche Vorschau wird vorbereitet.`

Do not show fake precision or false time estimates.

Preview:

- one genuine generated artwork;
- reduced resolution;
- visible but tasteful MEANINGFRAME watermark;
- no original high-resolution URL exposed;
- protected from search indexing;
- server-side delivery through short-lived access.

Copy:

> Dein erster MEANINGFRAME-Entwurf

Supporting line:

> Diese Vorschau zeigt die künstlerische Richtung. Nach dem Kauf erhältst du drei verfeinerte Varianten und kannst eine davon gezielt überarbeiten lassen.

Actions:

- `Digital Edition wählen — CHF 49`
- `Signature Edition wählen — CHF 229`
- `Meaning Map anpassen`

A second free preview is not available simply because the Co-Author dislikes the style. Allow a replacement only for a verified technical failure such as a missing face, corrupt image or serious safety defect.

### Flow 6 — Checkout

Digital:

- product summary;
- price;
- personal-use licence summary;
- one included revision;
- privacy retention.

Signature:

- all digital benefits;
- 40 × 50 cm;
- black or natural frame;
- printed Curator’s Note;
- Swiss standard delivery;
- delivery-address collection;
- realistic production estimate obtained from configured operations settings.

Use Stripe-hosted Checkout or embedded Stripe UI in a PCI-safe pattern.

### Flow 7 — Refined variants

After successful webhook confirmation:

- create a generation job;
- produce three deliberately distinct but faithful variants;
- run automated technical and content QA;
- surface status in project;
- email when ready.

Variant labels are neutral:

- Interpretation 01
- Interpretation 02
- Interpretation 03

Do not label one as “best”.

Comparison tools:

- large individual view;
- side-by-side on desktop;
- symbols-used summary;
- zoom;
- no public URL.

### Flow 8 — Guided revision

The Co-Author selects one variant and chooses up to three guided change categories:

- likeness;
- colour and light;
- composition;
- strengthen/remove a symbol;
- emotional tone;
- other concise instruction.

The UI must explain:

> Eine Überarbeitung verfeinert den gewählten Entwurf. Sie beginnt kein vollständig neues Kunstwerk.

One revision is included. Further revision requires CHF 19 checkout.

### Flow 9 — Curator’s Note

Select:

- Personal & Warm — default
- Poetic
- Curatorial

Show a generated draft before final approval.

Allow edits to factual statements and one regeneration after a Meaning Map correction. Do not offer unlimited tone regeneration.

### Flow 10 — Final approval

Show:

- final artwork;
- Curator’s Note;
- edition/product summary;
- production-format warning if applicable;
- AI co-creation disclosure.

Approval:

> Ich habe Kunstwerk, Schreibweise und Curator’s Note geprüft und für die finale Auslieferung beziehungsweise den Druck freigegeben.

Physical production cannot begin without this approval.

### Flow 11 — Delivery and reveal

Digital project:

- final artwork files;
- Curator’s Note PDF;
- Certificate of Co-Creation PDF;
- private Reveal Page;
- expiry/retention date;
- delete-now action.

Signature project:

- same digital delivery;
- production status;
- tracking details;
- support link.

## 3. Reveal Page

The private Reveal Page should feel like opening a gallery gift:

1. optional Co-Author message;
2. artwork reveal;
3. artwork title;
4. Curator’s Note;
5. selected symbols and their meaning;
6. transparent `Co-created with AI` note;
7. optional, separately consented share action.

No recipient email is required in the MVP. The Co-Author shares the private link.

## 4. Admin flow

### Operations dashboard

Show:

- paid projects awaiting generation;
- generation failures;
- projects awaiting customer approval;
- Signature orders awaiting production;
- orders in production;
- shipped orders;
- deletion jobs requiring attention;
- refunds/reprints.

### Production bundle

Admin can download a ZIP containing:

- print artwork;
- print-ready Curator’s Note;
- production manifest JSON;
- low-resolution reference preview;
- order reference;
- no unnecessary raw customer answers or photos.

### Manual fulfilment

Admin:

1. validates production bundle;
2. submits to the approved print provider;
3. records provider order ID and cost;
4. updates status;
5. records tracking;
6. handles reprint/refund incident if required.

## 5. Error and recovery states

Required recoveries:

- lost network during session → autosaved resume;
- rejected image upload → reason and correction;
- AI timeout → retry without duplicate charge;
- failed preview → preserve project and retry idempotently;
- Stripe cancellation → return to project;
- webhook delay → honest “payment confirming” state;
- generation failure after payment → automatic retry then admin escalation;
- fulfilment issue → customer status and support path;
- deletion job failure → admin alert and retry record.

## 6. Accessibility

Required:

- WCAG 2.2 AA;
- keyboard operation;
- visible focus states;
- correct labels and errors;
- alt text for sample art;
- customer artwork alt text defaults to private generic wording;
- reduced motion;
- no colour-only state distinction;
- mobile touch targets of at least 44 × 44 px;
- progress and wait states announced to assistive technology.

