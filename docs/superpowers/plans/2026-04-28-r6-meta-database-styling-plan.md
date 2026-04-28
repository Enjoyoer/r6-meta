# R6 Meta Database Styling Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Neutralize the base data (Weapon, Operator) in the database table and emphasize attachments using plain colored text instead of pills.

**Architecture:** Modify the `renderTable` function in the HTML file to remove `db-pill` wrappers and category-colored row accents, applying theme colors directly to the attachment text instead.

**Tech Stack:** HTML/JS/CSS

---

### Task 1: Update renderTable Styling

**Files:**
- Modify: `g:\My Drive\Personal\AI\Projects\PC\R6S\resources\r6-attachment-meta-sidebar.html`

- [ ] **Step 1: Write the updated renderTable code**

In `renderTable()` (around line 939), remove the row border, neutralize the weapon text, and remove `.db-pill` wrappers for the attachments:

```javascript
function renderTable(){
  const tbody=document.getElementById('tableBody');
  if(!tbody) return;
  tbody.innerHTML='';
  filtered.forEach(d=>{
    const tr=document.createElement('tr');
    tr.innerHTML=`
      <td style="font-weight:700; color:var(--color-text)">${d.Weapon}</td>
      <td style="font-weight:600; color:var(--color-text-muted); opacity:0.8">${d.Operator}</td>
      <td style="font-weight:700; color:${getColor(d.Muzzle)}">${d.Muzzle}</td>
      <td style="font-weight:700; color:${getGripColor(d.Grip)}">${d.Grip}</td>
      <td style="font-weight:700; color:${getUBColor(d.Underbarrel)}">${d.Underbarrel}</td>
    `;
    tbody.appendChild(tr);
  });
  document.getElementById('resultsCount').textContent=`${filtered.length} result${filtered.length!==1?'s':''}`;
}
```

- [ ] **Step 2: Run test to verify it passes**

Run: Refresh the `r6-attachment-meta-sidebar.html` page in the browser.
Expected: The table rows no longer have a colored left border. The Weapon name is standard text color. The Muzzle, Grip, and Underbarrel columns are colored text without background pill boxes.

- [ ] **Step 3: Clean up dangling references (if any)**

Check if there are any other references to `db-pill` in the CSS that were left over. Note: We recently consolidated `.filter-pill` and `.db-pill`, but `.filter-pill` still needs those styles. Ensure the CSS still has `.filter-pill` working correctly as per previous changes. No further action may be needed if the CSS was already cleaned up.

- [ ] **Step 4: Commit**

```bash
git add resources/r6-attachment-meta-sidebar.html
git commit -m "style: neutralize database base data and color attachment text"
```
*(Note: If git is not initialized in this directory, skip the commit step.)*
