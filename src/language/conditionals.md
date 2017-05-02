---
title: Conditionals
template: language
id: language/conditionals
---

# Conditionals

Pug's first-class conditional syntax allows for optional parentheses. 

If you’re coming from Pug v1, you may now omit the leading `-`. Otherwise, it's identical (just regular JavaScript):

```pug-preview
- var user = { description: 'foo bar baz' }
- var authorised = false
#user
  if user.description
    h2.green Description
    p.description= user.description
  else if authorised
    h2.blue Description
    p.description.
      User has no description,
      why not add one...
  else
    h2.red Description
    p.description User has no description
```

Pug also provides the conditional `unless`, which works like a negated `if`.  The following are equivalent:

```pug-preview-readonly
\\\\\\\\\\ a.pug <
unless user.isAnonymous
  p You're logged in as #{user.name}
\\\\\\\\\\ b.pug >
if !user.isAnonymous
  p You're logged in as #{user.name}
```
