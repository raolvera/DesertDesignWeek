# CSS Architecture – Module 2

## Files

- index.html – the starter page with a few extra classes added
- styles.css – the main stylesheet, organized into cascade layers

---

## Submission note

### Layer order

@layer reset, base, layout, components, utilities, overrides;

Reset comes first so it doesn't accidentally messed with anything I actually wrote. Base holds all the custom properties and default element styles. Layout handles the big structural stuff like the header, hero, and grid. Components is where the reusable pieces live buttons, cards, the callout, and the form. Utilities are small single purpose classes I can drop anywhere. Overrides is intentionally tiny, just a couple of exceptions I couldn't avoid.

---

### Three token decisions

**1. --color-accent**
I didn't want to type the terracotta hex code all over the place. Pointing everything at one variable meant I could test different shades early on and only touch one line when I changed my mind.

**2. --focus-ring and --focus-ring-offset**
Having the focus style as a token felt weird at first but it paid off I applied it to buttons, inputs, and the global :focus-visible rule all from the same two variables. If I needed to change the ring color for contrast reasons I'd only update it once.

**3. --space-* scale**
I kept reaching for random numbers like padding: 12px 20px and things were starting to look inconsistent. Switching to a 4-point scale forced me to pick from a fixed set of values and the spacing ended up feeling more intentional.

---

### Where the CSS got easier to maintain

The .flow utility was the most useful thing I added. Before I had it, I was writing margin-bottom on individual elements inside .hero-content and .section-heading, and if I wanted to adjust the spacing I had to find each one. Now I just put class="flow" on the parent and the children space themselves out automatically. I can also override the gap amount with --flow-space without touching the utility itself.
