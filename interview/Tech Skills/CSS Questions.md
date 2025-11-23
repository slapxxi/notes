1. Explain the CSS cascade.

   > The cascade determines which style applies when multiple rules target the same element. It's based on origin, importance, specificity and source order.

2. What's specificity in CSS?

   > Specificity defines which rule has higher priority. Inline styles have the highest, followed by IDs, classes, and element selectors.

3. What's the difference between `relative`, `absolute`, `fixed` and `sticky` positioning?

   > - `relative` positioned relative to its normal position
   > - `absolute` relative to the nearest positioned ancestor
   > - `fixed` relative to the viewport
   > - `sticky` toggle between `fixed` and `relative` depending on scroll position

4. Flexbox vs Grid

   > Flexbox is one dimensional (row or column) and great for distributing space among items. Grid is two-dimensional, allowing control over both rows and columns simultaneously.

5. How does z-index works?

   > `z-index` defines stacking order for positioned elements (those with `position` other than `static`). Higher values appear above lower ones withing the same stacking context.

6. What is a stacking context?
   > A stacking context is a hierarchy that determines how elements are layered. It can be created by properties like `position`, `opacity`, or `transform`. Elements in different contexts don't overlap based on global z-index values.

