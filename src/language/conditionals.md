---
title: Conditionals
template: language
id: language/conditionals
---

# Conditionals

Pug's first-class conditional syntax allows for optional parentheses. 

If you’re coming from Pug v1, you may now omit the leading `-`. Otherwise, it's identical (just regular JavaScript):

You can use strict or loose equality (triple and double equals), as well as any valid expression for a JavaScript `if` statement

```pug-preview
- 
  var user = {
    37: { name: "Finn", description: "The Human", authorised: true },
    38: { name: "Marceline", description: "The Vampire Queen", authorised: false }
  }
  var id = 38
#user
  if user[id].description
    h2.green Description
    p.description= user[id].description
  if user[id].name === "Finn"
    h1.yellow Name
    p.name= user[id].name
  else if user[id].authorised
    h2.blue Description
    p.description.
      User has no description,
      why not add one...
  else
    h2.red Description
    p.description User is not Finn.
```

Pug also provides the conditional `unless`, which works like a negated `if`.  The following are equivalent:

```pug-preview-readonly
\\\\\\\\\\ a.pug <
unless user.isAnonymous
  p You're logged in as #{user[id].name}
\\\\\\\\\\ b.pug >
if !user.isAnonymous
  p You're logged in as #{user[id].name}
```
