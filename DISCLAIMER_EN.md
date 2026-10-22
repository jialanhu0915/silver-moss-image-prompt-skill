# Legal Notice and User Responsibility

[简体中文](DISCLAIMER.md) · **English**　　Last updated: 2026-10-22　　Applies to: v0.2.x onward

> **By using this project you confirm that you have read and agree to this notice.** This project is not responsible for any image produced from its prompts, nor for how you use such images. All legal risk is borne by the user. If you do not agree, do not use it. The English and Chinese versions are intended to say the same thing; if you find a discrepancy, please open an issue in the repository.

## 1. What this is and is not

1. This project is a **prompt-writing method** in Markdown. It contains no model, no weights, no scripts, and generates no images. Images are produced by MOSS-Image (or another model) that the user deploys or calls.
2. It is **not an OpenMOSS project** and is not endorsed, authorized or reviewed by OpenMOSS. OpenMOSS and the upstream repository are not responsible for this project, and it does not represent their views (see [NOTICE.md](NOTICE.md)).
3. It is **not legal advice**. The laws listed here are pointers only and may be incomplete, inaccurate or out of date. Consult official texts and a qualified lawyer in your jurisdiction.

## 2. Content filtering: not imposed by default

1. This project does **not require** `nsfw` or similar filter terms in negative prompts. Private, offline, access-controlled deployments have lawful uses, and filtering policy is for the operator to decide.
2. A negative-prompt `nsfw` tag is only a soft bias on sampling. It is **not a content filter** and is no substitute for moderation or age verification; omitting it means the model has no extra suppression in that direction. Add it back if you want more conservative output, but real filtering must be done at the deployment layer.
3. Consequently, **whether to generate, display or distribute adult or other sensitive content is decided and borne entirely by the user.** For public services, shared environments, or any setting involving minors, the user must add their own content filtering, age verification and moderation.
4. This project makes no warranty about the legality, appropriateness, truthfulness or safety of generated content, and has **no ability** to review any individual generation.

## 3. Prohibited uses (red lines)

The following are not supported, and the user must not use any part of this project for them:

| Category | Description |
| :--- | :--- |
| **Sexual content involving minors** | Any sexual, pornographic or sexualized content depicting a minor, or a character who appears childlike or underage. **This applies whether the character is real, fictional, anime-style or AI-generated, and regardless of any stated, claimed or "actual" age.** Many jurisdictions criminalize such images, including fictional and synthetic ones, and "no real victim" is not a defense |
| **Real persons without consent** | Using a real person's likeness, voice or identity to create sexual or nude content, defamation, fabricated evidence, or for fraud, impersonation, harassment or retaliation (including face-swap "deepfakes") |
| **Unlawful content** | Child sexual abuse material, terrorist or extremist propaganda, incitement to violence or hatred, illegal trade and scams, content harming national security or public interest, and anything else prohibited where you are |
| **Infringement** | Infringing copyright, trademark, likeness, reputation, privacy or personal-data rights; using the name of a brand, institution or public figure to publish misleading content |
| **Deceptive use** | Passing AI-generated content off as real photographs, news, evidence or official documents without disclosure |

These red lines govern **conduct**; they are not an added condition of the license and do not alter the rights granted by Apache-2.0. Anyone who violates them bears all consequences.

Separately, the maintainers' day-to-day discretion over this repository (whether to answer a request, merge or remove a contribution) is repository governance and is unrelated to the rights the license grants.

## 4. User responsibilities

The user is **solely and fully** responsible for:

1. **Compliance** with all applicable laws where content is generated, stored, shown, distributed or monetized, and where the audience is located, including without limitation:
   - Mainland China: Criminal Law arts. 363–367 (obscene materials), Cybersecurity Law, Personal Information Protection Law, Law on the Protection of Minors, Civil Code (likeness, reputation, privacy), Copyright Law, Interim Measures for Generative AI Services, Provisions on Deep Synthesis, Measures for Labeling AI-Generated Content;
   - United States: federal and state laws on child sexual abuse material and obscenity (e.g. 18 U.S.C. §§ 2251, 2252, 2252A, 1466A), non-consensual intimate imagery (e.g. the TAKE IT DOWN Act and state laws), right of publicity and anti-fraud law;
   - EU and UK: AI Act transparency and deepfake-labeling duties, GDPR, DSA, the UK Online Safety Act 2023 and criminal law on images of children;
   - the law of any other jurisdiction where you or your audience are located.
2. **Labeling** AI-generated content, explicitly and implicitly, as required by law or platform rules.
3. **Lawful inputs.** You must have the right to use any prompt, reference image, tag, name, brand or character you enter. Do not enter other people's personal information.
4. **Deployment and access control**, including age verification, access limits, logging and handling of reports.
5. **Model and third-party licenses.** MOSS-Image weights, LoRAs, base models and tools carry their own licenses and terms (possibly including use restrictions). Confirm and follow them; this project's Apache-2.0 does not cover them.
6. **Platform rules** wherever you publish.
7. **Your own judgment.** Examples, templates, term lists and self-checks here are writing aids, not a substitute for your own compliance review.

## 5. Ownership and risk of generated content

1. **Copyright status is uncertain.** Jurisdictions differ, and are still changing, on whether AI output is protected and who owns it. No warranty is given about any image.
2. **Output may resemble existing works.** The model may produce content close to existing works, characters, people or trademarks. This project does not guarantee non-infringement or provide rights clearance.
3. **Artist and style terms.** This project does not encourage copying a living artist's style by name; whether such use infringes is for the user to judge and bear.
4. **Text in images.** Text, logos, brands and names inside an image may raise trademark, defamation or false-advertising risk.

## 6. No warranty

To the maximum extent permitted by law, this project and all of its content are provided **"AS IS"**, without warranty of any kind, express or implied, including but not limited to merchantability, fitness for a particular purpose, accuracy, completeness, non-infringement, continued availability, compatibility with any model version, or that results will match expectations. Rules here derive from official documentation, general knowledge and the author's experience; many have not been tested under controlled conditions (see the evidence levels in [references/diagnostics/sources.md](references/diagnostics/sources.md)), may be wrong, and may become outdated with upstream changes. This section supplements, in the spirit of, sections 7 and 8 of the [LICENSE](LICENSE).

## 7. Limitation of liability

To the maximum extent permitted by law, in no event shall the authors, contributors or copyright holders be liable for **any direct, indirect, incidental, special, punitive or consequential damages arising from the use of, or inability to use, this project, or from any content generated with its assistance**, including but not limited to legal liability, administrative penalties, criminal prosecution, third-party claims, account or service suspension, loss of goodwill, loss of profit, data loss and emotional distress, whether in contract, tort (including negligence), strict liability or otherwise, and even if advised of the possibility of such loss.

Liability that cannot lawfully be excluded or limited is preserved only to the minimum extent the law requires.

## 8. Indemnification

The user agrees to bear, and to indemnify and hold harmless the authors and contributors from, any claim, loss, liability, fine and expense (including reasonable attorneys' fees) arising from the user's use of this project, breach of this notice or applicable law, or infringement of third-party rights.

## 9. Minors and descriptions of age

1. The text of this project is intended for adult users. Minors should use it under guardian supervision and must not use it for anything listed in section 3.
2. This project includes methods for describing a subject's age and appearance (for example "two-sided exclusion" to keep a figure from looking too old or too young). These are **image-control techniques**, not permission to sexualize a person of any age, and do not imply that stating an age makes content lawful.

## 10. Third-party material, links and trademarks

1. Upstream material cited here (OpenMOSS/MOSS-Image USERGUIDE, README, etc.) belongs to its rights holders under Apache-2.0; see [NOTICE.md](NOTICE.md). Where upstream changes, the official documentation controls.
2. Products, models, software, camera models, brands, works and artist names mentioned are the property of their owners and appear for descriptive purposes only, implying no affiliation, sponsorship or endorsement.
3. External links are a convenience; this project is not responsible for their content.

## 11. Privacy and data

This project collects, uploads and stores no user data and has no telemetry. The models, APIs and platforms you use may; read their privacy policies. Do not enter other people's personal or sensitive information, or confidential material, in prompts.

## 12. Relationship to the license

This project is licensed under [Apache License 2.0](LICENSE). This notice states the disclaimer scope, user responsibilities and project position; it **neither modifies nor restricts the rights Apache-2.0 grants you**. Sections 7 (disclaimer of warranty) and 8 (limitation of liability) of Apache-2.0 continue to apply, and this notice supplements and specifies them.

## 13. General

1. **Severability.** If any provision is held invalid or unenforceable, the rest remains in force, and that provision is to be read to the maximum extent permitted by law according to its intent.
2. **No waiver.** Failure or delay in exercising any right is not a waiver.
3. **Changes.** This notice may be updated as the project or the law changes; continued use means acceptance. Earlier versions are in git history.
4. **Governing law and disputes.** Subject to mandatory rules, disputes arising from this notice are governed by the laws of the People's Republic of China (excluding conflict-of-law rules), with the competent people's court at the defendant's domicile having jurisdiction. Mandatory consumer or other protections in your jurisdiction are unaffected.
5. **Reporting.** If you find this project's content being used for anything in section 3, or infringing material in its documents, open an issue in the repository or contact the maintainers as listed on the repository page. For child sexual abuse material, report to local law enforcement and to bodies such as NCMEC, the IWF or China's Illegal and Harmful Information Reporting Center, rather than posting it publicly.
