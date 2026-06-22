---
name: iconoir-react
description: How to use the iconoir-react library for SVG icons in React projects. Make sure to use this skill whenever the user asks to add an icon, mentions Iconoir, wants to implement SVG icons in a React/Next.js app, needs help with iconoir-react components and props, or wants to set up global icon styles using IconoirProvider.
---

# Iconoir React

Iconoir is an open-source library with 1300+ unique SVG icons designed on a 24x24 pixel grid. This skill covers the `iconoir-react` package, which exports these icons as React components.

## Installation

When the user needs to install the package, use their preferred package manager:

- **npm**: `npm i iconoir-react`
- **Yarn**: `yarn add iconoir-react`
- **pnpm**: `pnpm add iconoir-react`

## Basic Usage

Icons are imported as individual React components. 

```jsx
import { Iconoir } from 'iconoir-react';
import React from 'react';

function App() {
  return <Iconoir />;
}

export default App;

```

### Props

Icons can take any standard SVG properties as optional props.
Example: `<Iconoir color="red" height={36} width={36} />`

**Default values for common props:**

* `color`: `"currentColor"`
* `width`: `"1.5em"`
* `height`: `"1.5em"`
* `strokeWidth`: `1.5`

## Setting Global Defaults (IconoirProvider)

When the user wants to apply consistent styling across multiple icons, always recommend and use `IconoirProvider`. This prevents repeating props for every single icon.

Wrap the container or application with `<IconoirProvider>` and pass an `iconProps` object:

```jsx
import { Check, IconoirProvider } from 'iconoir-react';

export default function App() {
  return (
    <IconoirProvider
      iconProps={{
        color: '#AAAAAA',
        strokeWidth: 1,
        width: '1em',
        height: '1em',
      }}
    >
      <SomeOtherContainer>
        {/* This Check icon will inherit the props defined in the Provider */}
        <Check />
      </SomeOtherContainer>
    </IconoirProvider>
  );
}

```

## Component Naming Conventions

When guessing or generating the name of an icon component, you must adhere to Iconoir's specific naming conventions.

**Rule 1: PascalCase**
React components are always named as `PascalCase` variations of their reference names.

* *Example:* `airplane-helix-45deg` becomes `<AirplaneHelix45deg />`

**Rule 2: Object-Oriented Hierarchy**
Icons follow an object-oriented naming convention (`[Object]-[Modifier]-[Container]`), rather than action-based naming.

* *Example:* Use `<UserMinus />`, do NOT use `<RemoveUser />`.
* *Example:* Use `<CheckCircle />`

**Rule 3: Modifiers and Containers**

* **Modifiers:** Added as a secondary object (e.g., `-plus`, `-minus`, `-warning`, `-check`, `-xmark`, `-tag`, `-ban`, `-slash`).
* *Note:* `-plus-in` and `-minus-in` are used when the plus/minus is inside the main object.


* **Containers:** Shapes used as a container (`-square`, `-circle`).
* *Example:* `<UserMinusSquare />` (User is the object, minus is the modifier, square is the container).

**Rule 4: Solid Icons**
Iconoir offers Regular and Solid icons. For solid icons, the reference name ends with `-solid`, meaning the React component will end with `Solid`.

* *Regular:* `<CheckCircle />`
* *Solid:* `<CheckCircleSolid />`

**Rule 5: Physical Actions (Exception)**
Icons representing physical actions *can* embed the action in their name.

* *Examples:* `<Walking />`, `<Running />`, `<VehicleFast />`, `<CraneLifting />`.
