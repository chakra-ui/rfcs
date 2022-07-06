- Start Date: 2022-07-26
- Target Major Version: 2.x
- Reference Issues: 
- Implementation PR: 

# Summary

I've build a bunch of components in Saas UI that I think are essential to any UI library, but weren't part of Chakra UI yet.
I noticed some of them are listed on the roadmap, so I thought it would be a great idea to consolidate them to Chakra UI.

The first component I like to propose is `LoadingOverlay`.
It's a loading indicator that fills or overlays it's parent and renders a spinner in the center.

# Basic example

```tsx
<Box height="400px">
  <LoadingOverlay>
    <LoadingSpinner />
    <LoadingText>Loading...</LoadingText>
  </LoadingOverlay>
</Box>
```

# Motivation

When building apps different parts of the UI often requires a loading state.
The Spinner component is suitable for a lot of situations, eg in Buttons, but using it in larger components,
like cards or pages, requires you to do extra work to position it properly and add transitions effects.
With a LoadingOverlay we can improve the DX and development speed.

# Detailed design

The design I propose includes multiple variants that handle different ways of positioning the overlay.
Support all spinner properties and custom spinners.

# Import

The LoadingOverlay and it's child components live in the spinner package.

```
import { LoadingOverlay, LoadingSpinner, LoadingText } from '@chakra-ui/spinner'
```

# Usage

## Default

The default variant is "fill", the loader tries to fill it parent with flex="1" and height="100%".

```tsx
<LoadingOverlay>
  <LoadingSpinner />
  <LoadingText>Loading...</LoadingText>
</LoadingOverlay>
```

## Overlay

The overlay variant uses position="absolute" and inset="0" to overlay it's parent.
This requires you to set position="relative" on the parent to make sure it is positioned correctly.

```tsx
<LoadingOverlay variant="overlay">
  <LoadingSpinner />
  <LoadingText>Loading...</LoadingText>
</LoadingOverlay>
```

## Fullscreen

The fullscreen variant positions the overlay fixed on top of you app.

```tsx
<LoadingOverlay variant="fullscreen">
  <LoadingSpinner />
  <LoadingText>Loading...</LoadingText>
</LoadingOverlay>
```

## isLoading

The loader can be hidden by setting isLoading to false, the default value is true. 
Changing the value will show/hide the loader with a fade transition.

```tsx
<LoadingOverlay variant="fullscreen" isLoading={false}>
  <LoadingSpinner />
  <LoadingText>Loading...</LoadingText>
</LoadingOverlay>
```

## motionPreset

The container element is a MotionBox and rendered with AnimatePresence, so it supports transitions.
The transition can be customized by setting the motionPreset property.

```tsx
<LoadingOverlay variant="fullscreen" motionPreset="slideInUp">
  <LoadingSpinner />
  <LoadingText>Loading...</LoadingText>
</LoadingOverlay>
```

## Customizing the Spinner

The LoadingSpinner accepts all Spinner props.

```tsx
<LoadingOverlay>
  <LoadingSpinner size="lg" color="primary.500" thickness="4px" />
  <LoadingText>Loading...</LoadingText>
</LoadingOverlay>
```

## Custom Spinner

```tsx
<LoadingOverlay>
  <CustomSpinner />
  <LoadingText>Loading...</LoadingText>
</LoadingOverlay>
```

## Styling

LoadingOverlay accepts all Box props, it positions children in the center by default.

```tsx
<LoadingOverlay justifyContent="flex-start">
  <LoadingSpinner />
  <LoadingText>Loading...</LoadingText>
</LoadingOverlay>
```

# A11y

If not using visibile loading text add a `label` to the Spinner add a loading text that is visible to screen readers.

Add a containerRef to make sure the container has `aria-live` and `aria-busy` to indicate that the content within that region is changing and when it's done screen readers can announce the updates.

```tsx
function Page() {
  const containerRef = React.useRef()
  return (
    <Box ref={containerRef}>
      <LoadingOverlay containerRef={containerRef}>
        <LoadingSpinner />
        <LoadingText>Loading...</LoadingText>
      </LoadingOverlay>
    </Box>
  )
}
```

# Drawbacks

I don't see any drawbacks.

# Alternatives

I'm open for any other ideas of improvements.

# Adoption strategy

It's not a breaking change, so it can be released without any issues.

# Unresolved questions

Optional, but suggested for first drafts. What parts of the design are still
TBD?
