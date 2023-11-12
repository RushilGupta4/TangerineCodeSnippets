# Implementation of Advanced Feautres in Tangerine

---

## Overview

This documentation provides simple code snippets for users with limited technical knowledge to implement advanced features in [Tangerine](https://www.tangerinecentral.org/).

## Table Of Contents

1. [Randomization of Sections](#randomization-of-sections)

2. [Auto-Stop Timed Grids](#auto-stop-timed-grids)

3. [Last Steps: Testing](#last-steps-testing)

<div style="page-break-after: always;"></div>

## Randomization of Sections

---

### Choose Randomization Type

There are 2 ways to randomize sections: (1) Randomly choose one section from a given set (Example: section 1 out of 30) or (2) Choose a set of sections from a given set of such sets (Example: set 1 out of 4).

### Option 1: Randomly Choosing a Section

Insert the following code into the on-open section:

```javascript
window.chosenSection = null;
```

Insert the following code into the on-change section:

```javascript
const sections = [
    'Section1',
    'Section2',
    ... // All the sections that need to be randomized
];

if (!window.chosenSection) {
    window.chosenSection = sections[Math.floor(Math.random() * sections.length)];
}

for (let i = 0; i < sections.length; i ++) {
    let section = sections[i];
    if (section == window.chosenSection) {
        sectionEnable(section);
    } else {
        sectionDisable(section);
    }
}
```

### Option 2: Randomly Choosing a Set of Sections

Insert the following code into the on-open section:

```javascript
window.chosenSet = null;
```

Insert the following code into the on-change section:

```javascript
const noSets = 5; // Add number of sets you have here

const sectionsInSet = [
    'Section1_Set{set}',
    'Section2_Set{set}',
    ... // All the sections that are a part of each set
];

if (!window.chosenSet) {
    window.chosenSet = Math.ceil(Math.random() * window.noSets);
}

for (let set = 1; set <= noSets; set ++) {
    for (let i = 0; i < sectionsInSet.length; i ++){
        let section = sectionsInSet[i].replace("{set}", set);
        if (set == window.chosenSet) {
            sectionEnable(section);
        } else {
            sectionDisable(section);
        }
    }
}
```

<div style="page-break-after: always;"></div>

## Auto-Stop Timed Grids

---

### Pre-Steps

Go to the edit HTML option of Tangerine, and copy the code to any desirable code editor, like VSCode. If you aren't comfortable with code editors, proceed to edit the HTML within the given input box.

_Note: Make sure to save a copy of the HTML file (copy and paste the HTML to a .txt file)_

### Code Snippet

Find the correct `<tangy-timed>` element in the HTML by searching for the variable's name in the HTML until you find the correct `<tangy-timed>` element. Now, insert the following code into the `<tangy-timed>` element you found!

```javascript
onchange="
    if (1 == 1) {
        const buttons = this.shadowRoot.querySelectorAll('tangy-toggle-button');
        let count = 0;
        let threshold = 4; // Number of consecutive words inccorect

        for (let i = 0; i < buttons.length; i++) {
            if (buttons[i].pressed) {
            count++;
            if (count >= threshold) {
                break;
            }
            } else {
            count = 0;
            }
        }

        if (count >= threshold) {
            this.duration = 0;
            setInterval(() => {
            this.duration = 60;
            }, 1000);
        }
    }
"
```

### Example

Here is an example of what your `<tangy-timed>` element would look like once you have added the code.

```javascript
<tangy-timed
  ... // pre-exsiting code
  onchange="
    if (1 == 1) {
        const buttons = this.shadowRoot.querySelectorAll('tangy-toggle-button');
        let count = 0;
        let threshold = 4; // Number of consecutive words inccorect

        ... // the reamining code from above
    }
"></tangy-timed>
```

<div style="page-break-after: always;"></div>

# Last Steps: Testing

---

Test your assessment tool to ensure that desired features are functional, and experiment yourself by editing! Feel free to experiment with and modify the content or code snippets according to your requirements.

Moreover, if you have any issues or problems, please feel free to contact me at [rushilgupta4@gmail.com](mailto:rushilgupta4@gmail.com).

By [Rushil Gupta](https://rushilgupta.tech)
