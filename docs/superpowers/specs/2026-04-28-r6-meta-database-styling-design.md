# R6 Meta Database Styling Redesign

## Purpose
To reduce visual noise in the R6 Attachment Meta dashboard's data table. By neutralizing the base data (Weapons and Operators) and emphasizing only the tactical attachments (Muzzle, Grip, Underbarrel), the dashboard enables faster scanning of meta trends without the chaotic "rainbow effect."

## Architecture & Changes

### Neutral Base Data
- **Weapon Names:** Change from category-colored text to high-contrast monochrome (e.g., `var(--color-text)`).
- **Operator Names:** Remain a muted, slightly lower-opacity monochrome.
- **Row Accents:** Remove the category-colored left-border accent from the table rows (`<tr>`).

### Emphasized Attachments
- **Attachment Names:** Maintain their high-weight, vibrant colors based on their specific themes.
- Muzzle text remains colored via `getColor()`.
- Grip text remains colored via `getGripColor()`.
- Underbarrel text remains colored via `getUBColor()`.

## Data Flow & State
No changes to the underlying `DATA` structure or filtering logic. This is purely a presentation-layer inline-style update inside the `renderTable()` function.

## Testing
- Verify that standard loadout rows display neutral weapon names and vibrant attachment names.
- Verify that the table structure remains aligned and readable.
