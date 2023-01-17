- Start Date: 2023-01-17
- Target Major Version: 3.x
- Reference Issues: -
- Implementation PR:

# Summary

This RFC proposes a new way to define or change styleConfig / themes of components.

# Basic example

```tsx
<Button
  styleConfig={({ theme, variant, size }) => ({
    baseStyle: {
      rounded: true,
    },
    variants: {},
    sizes: {
      md: {
        px: 4,
        py: 2,
      },
    },
  })}
>
  Styled button
</Button>
```

# Motivation

The current implementation of theming requires a good understanding of Chakra UI's internals.
It has a high learning curve, Typescript/auto complete support is very poor.
Aside from that it comes with the downside that are theme styles are like global css styles,
changing them can have unintended consequences on parts of the application that are not directly obvious.

With the introduction of the ChakraBaseProvider we now have more flexibility to define theming
for our components, and it's a good time to start thinking how to improve the theming process for v3.

# Detailed design

TBD

# Drawbacks

# Alternatives

# Adoption strategy

The change could be introduced without breaking anything, unless this would be made the default way to style components in v3.

# Unresolved questions

- Should there be 'unstyled' components?
- Should components include all default variants?
