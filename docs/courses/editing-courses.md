# Creating and editing LibreLingo courses

LibreLingo courses consist of files that contain course content. These files
are organized in a specific directory structure.

A simplified example of the directory structure of a LibreLingo course:

```
courses/french-from-english/
courses/french-from-english/basics
courses/french-from-english/basics/module.yaml
courses/french-from-english/basics/skills
courses/french-from-english/basics/skills/hello.yaml
courses/french-from-english/course.yaml
```

LibreLingo courses can be published in different formats. One such format is
the LibreLingo web app.

When you are working with LibreLingo courses, you'll be mostly editing the
`.yaml` files as seen above. The standard way of editing LibreLingo courses is
using GitHub.

If you don't know how to use GitHub, it might be useful to check out these
guides:

- [Creating new files on GitHub](https://docs.github.com/en/github/managing-files-in-a-repository/creating-new-files)
- [Editing files on GitHub](https://docs.github.com/en/github/managing-files-in-a-repository/editing-files-in-another-users-repository)

## Editing skills

If you are contributing to existing courses, the thing you are most likely
to do is edit existing skills.

Skills are written as YAML files with a specific structure. From our example
above, the YAML file corresponding to the "hello" skill would be
`courses/french-from-english/basics/skills/hello.yaml`.

The structure of `hello.yaml` is as follows:

```yaml
Skill:
  Id: 33bfee7d-de74-4362-bf15-ce165add2dc8
  Name: Hello
  Thumbnails:
    - people1
    - woman1
    - man1

New words:
  - Word: l'homme
    Translation: the man
    Images:
      - man1
      - man2
      - man3

  - Word: la femme
    Synonyms:
      - la dame
    Translation: the woman
    Also accepted:
      - the female

Phrases:
  - Phrase: La femme dit bonjour
    Alternative versions:
      - la femme dit salut
    Translation: The woman says hello
    Alternative translations:
      - The woman says hi

  - Phrase: L'homme dit bonjour
    Alternative versions:
      - L'homme dit salut
    Translation: The man says hello
    Alternative translations:
      - The man says hi

Mini-dictionary:
  French:
    - dit: says
    - bonjour:
        - hello
        - hi
    - L'homme: the man

  English:
    - says: dit
    - hello:
        - bonjour
        - salut
```

While the meaning of this file should be relatively straight-forward, here's
a couple things to keep in mind:

- `Skill:`
  - `Id:` never change this value. This value identifies the skill uniquely, thus changing it will effectively create a new skill and delete the old one.
  - `Thumbnails:` these thumbnails can be used to illustrate the skill on the course summary page

### By example

For example, this is how you'd want to add a new alternative version to the
phrase "La femme dit bonjour":

```diff
Phrases:
  - Phrase: La femme dit bonjour
    Alternative versions:
      - La femme dit salut
+     - La madame dit salut
    Translation: The woman says hello
    Alternative translations:
      - The woman says hi
```

Keep in mind that when you add a new phrase, or a new version or translation
to a phrase, it's not automatically updating to the mini-dictionary. So you'd
want to add any new words there:

```diff
Mini-dictionary:
  French:
    - dit: says
+   - madame: lady
    - bonjour:
      - hello
      - hi
    - L'homme: the man
```

### Creating new skills

Creating new skills is a matter of creating their corresponding YAML file.
That being said, there are a couple things to keep in mind:

- Skills should have a unique `Id`. Such identifiers can be generated using
  [this website](https://www.uuidgenerator.net/version4).
- Before skills will actually show up in the web app, they need to be added to
  a module. See the section below.

## Editing modules

Modules are simply groups of skills. Their YAML files are quite straightforward.

See `courses/french-from-english/basics/module.yaml` from the example above:

```yaml
Module:
  Name: Basics

Skills:
  - hello.yaml
```

Keep in mind that the order in which the skills appear in this YAML file is
the order they are meant to appear in the web app as well.

### Creating new modules

As with creating new skills, creating new modules is also mainly about creating
their corresponding YAML file. You have to keep in mind that the module will
only show up in the web app, if it's also listed in the course's
`course.yaml` file. Here's how you'd add it:

```diff
Course:
  Language:
    Name: French
    IETF BCP 47: fr
  For speakers of:
    Name: English
    IETF BCP 47: en
  License:
    Name: CC BY 3.0
    Short name: CC BY 3.0
    Link: https://creativecommons.org/licenses/by/3.0/

Modules:
  - basics/
+ - animals/
```
