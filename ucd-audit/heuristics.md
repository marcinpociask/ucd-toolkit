# Audit reference

## Severity scale (Nielsen)

| Rating | Meaning |
|---|---|
| 0 | Not a usability problem |
| 1 | Cosmetic: fix if time allows |
| 2 | Minor: low priority |
| 3 | Major: high priority, fix before release |
| 4 | Catastrophe: must fix before release |

Rate from three factors: how often it occurs, how hard it is to overcome, and whether it keeps recurring for the same user.

## Nielsen's 10 heuristics: what to check

1. **Visibility of system status** – Loading, progress and saved states shown? Current location in navigation clear? Feedback after every action? Selected and active states distinguishable?
2. **Match between system and the real world** – Language the user would use, no internal jargon? Icons recognisable or labelled? Information in a natural order? Units, dates and formats familiar?
3. **User control and freedom** – Back, cancel, close and undo available? Can a multi-step flow be left and resumed? Destructive actions reversible or confirmed?
4. **Consistency and standards** – Same component for the same job everywhere? Same label for the same action? Platform conventions followed (iOS, Android, web)? Tokens used consistently?
5. **Error prevention** – Constraints and sensible defaults? Dangerous actions separated from frequent ones? Confirmation for irreversible steps? Input formats shown before the error happens?
6. **Recognition rather than recall** – Options visible instead of memorised? Context carried between steps? Recent or suggested items offered? Labels persistent (not placeholder-only)?
7. **Flexibility and efficiency of use** – Shortcuts or accelerators for frequent tasks? Bulk actions where relevant? Sensible defaults? Path for both novice and expert?
8. **Aesthetic and minimalist design** – One clear primary action per view? Hierarchy matches importance? Anything that could be removed without loss? Density appropriate for the task?
9. **Help users recognise, diagnose and recover from errors** – Error state designed at all? Message says what happened and what to do, in plain language, next to the problem? Input preserved after an error?
10. **Help and documentation** – Onboarding or empty-state guidance? Contextual help for complex inputs? Help reachable without losing place?

## Accessibility quick checks (WCAG 2.2 AA)

- **Text contrast** – 4.5:1 for normal text, 3:1 for large text (≥ 24 px, or ≥ 18.66 px bold). (1.4.3)
- **Non-text contrast** – 3:1 for UI component boundaries, icons and state indicators. (1.4.11)
- **Use of colour** – Colour is never the only signal for state, error or meaning. (1.4.1)
- **Target size** – At least 24×24 CSS px (2.5.8); recommend 44×44 pt on iOS and 48×48 dp on Android per platform guidance.
- **Focus** – Visible focus state designed for every interactive element; not obscured by sticky elements. (2.4.7, 2.4.11)
- **Labels** – Every input has a persistent visible label; icon-only buttons have an accessible name noted. (3.3.2, 4.1.2)
- **Text resize and reflow** – Layout survives 200% text and long or translated strings. (1.4.4, 1.4.10)
- **Error identification** – Errors described in text and associated with the field. (3.3.1, 3.3.3)
- **Motion** – Non-essential animation can be reduced. (2.3.3 is AAA; note as advisory)
- **Reading and focus order** – Layer and layout order produce a logical sequence. (1.3.2, 2.4.3)

## Component checklist

- States: default, hover, pressed, focus, disabled, loading, error, selected (as applicable)
- Variants and properties named consistently; no duplicate variants; booleans used for toggles
- Colours, type, spacing and radius bound to variables or styles, not hard-coded
- Auto layout behaves with short and long content; min and max widths considered
- Description or usage note present

## Flow checklist

- Clear entry point and a clear end state confirming success
- Number of steps justified; nothing asked that is not needed
- Progress shown for more than two steps
- Every step has a way back; data is kept when going back
- Error and empty paths designed, not only the happy path
- Same patterns and labels used from step to step
