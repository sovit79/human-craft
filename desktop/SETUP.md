# Installing Human Craft in Claude Desktop

Claude Desktop (Pro/Team) supports Projects — custom instructions + uploaded files that persist across conversations.

## Writing skill setup

**Step 1: Create a project**
Claude Desktop → Projects → New Project → name it "Human Craft — Writing"

**Step 2: Add custom instructions**
Project Settings → Custom instructions → paste the contents of `desktop/project-instructions.md`

**Step 3: Upload skill files**
Project → Add files → upload all files from the `desktop/writing/` folder:
- `SKILL.md`
- `taxonomy.md` (English tells — always upload)
- `playbook.md` (English fix recipes — always upload)
- `taxonomy-ko.md` *(optional — Korean tells)*
- `taxonomy-zh.md` *(optional — Chinese tells)*
- `taxonomy-es.md` *(optional — Spanish tells)*
- `taxonomy-ar.md` *(optional — Arabic tells)*
- `taxonomy-pt.md` *(optional — Portuguese tells)*

**Step 4: Use it**
In the project, type `humanize` and paste your text. Done.

---

## Design skill setup

**Step 1:** Create project → "Human Craft — Design"

**Step 2:** Custom instructions → paste `desktop/project-instructions.md`

**Step 3:** Upload all files from `desktop/design/`:
- `SKILL.md`
- `taxonomy.md`
- `playbook.md`

**Step 4:** Type `humanize` and paste your HTML/CSS/React.

---

## Combined project (writing + design + image)

Upload all files from both `desktop/writing/` and `desktop/design/` into one project.
The custom instructions handle routing automatically based on what you paste.

---

## Updating

When the repo updates, re-download the files and re-upload to your project.
Watch [github.com/sovit79/human-craft](https://github.com/sovit79/human-craft) for releases.
