# **Problem**
- Every time we want claude to do something we have to tell it again and again.
- We also want response in different format such as in JSON or in certain way, we explain it to claude and it's repetitive.
- Such as `I want you to explain me about "Apple". Make sure you don't include emojis or verbose wording. (using or containing more words than are necessary to express an idea).`
- If you open this in one chat, claude will follow it. But let's say if you open another chat and ask claude to do the same without mentioning your requirement, it'll not give the response the way you want.
- However, `skills` fix this.

---

# **What are skills?**
- A skill is a markdown file that teaches claude how to do something and claude automatically applies that knowledge whenever it's relevant.
- Agent skills are `folders` of `instructions`, `scripts` and `resources` that agents can discover and use to do things more accurately and efficiently.

# **Format of a skill markdown file**
```javascript
---
name: pr-review

description: Reviews pulls requests for code quality. Use when reviewing PRs or checking code changes. // this is how claude decides whether to use the skill
---

When reviewing code in this FastAPI project, check for:

## Code quality
1. **Readability and clear naming** - Variables, functions, and classes descriptive names.
2. **Consistent patterns** - Follow the existing router/schema/model for the codebase.
3. **No hardcoded secrets** - Ensure API Keys, tokens, and secrets use variables.
```

# **Example**
- Folder structure.
```text
└── claude
    └── skills
        └── pr-review
            └── SKILL.md
```
- The above skill content is in this `SKILL.md` file.
- Then, you asked Claude with the following prompt, `Can you review the pull request on branch sg-221?`. When you ask the Claude to review this PR, it matches your request against available skill descriptions and finds this one.
- Claude reads your requests, compare it to all available skill `"descriptions"`, and activates the ones that match.

# **Skill Storage**
- You can store skills in a few places depending on who needs them.
- Project skills go in the home/root directory `.claude/skills`.
- `cd .claude/skills`
- `ls`
```bash
-- commit-message
-- debugging
-- documentation
-- pr-description
```
- and it follows you across all your project.
- Each of these directories, have a `SKILL.md` file which has the name, description and proper instructions.
- Skills are automatic and task-specific.
- You can upload this skill to github repo. One who clones this repo, gets these skills automatically.
- This is where the team standards live, like your company's brand guidelines, preferred fonts, and colors, and colors that you use for web design. Basically, anything which you want the Claude AI to follow generally.

# **What is "CLAUDE.md" file?**
- Skills are unique, because they're automatic and task-specific.
- `CLAUDE.md` files load into every conversation.
- For example, if you want Claude to always use TypeScript strict mode, it goes in the `CLAUDE.md` file.
- Skills on the other hand, load on demand when they match your request. It only loads when the prompt match your name and description, so it doesn't fill your entire context window.

    # **Why so?**
    - Your PR review checklist doesn't need to be in the context when you are debugging.
    - It only loads when you actually ask for a review.

# **When to use Skills**
- Skills works best for specialized knowledge that applies for specific tasks.
- If you want claude to do certain tasks for a certain topic, it's a skill that needs to be written.