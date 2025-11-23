**Q: Explain the difference between controlled and uncontrolled components.**

 Controlled components are managed by React state - the UI reflects the state. Uncontrolled components rely on the DOM itself for state, accessed via refs.  Controlled components are preferred for predictable state management.

**Q: What's the purpose of React keys?**

 Keys help React identify which elements have changed, been added, or removed. Without stable keys, React may re-render or misplace elements inefficiently.

**Q:  What are React hooks and why they were introduced?**

 Hooks let you use state and other React features without writing class components. They were introduced to simplify code reuse and reduce complexity in managing lifecycle logic.

**Q: How does React reconciliation work?**

 React uses a virtual DOM to compare the new and previous render trees. It calculates the minimal number of changes required and efficiently updates only those DOM nodes.

 The process React uses to determine how the UI should update when the application's state or props change.
 
 1. **Virtual DOM comparison**
	 At a high level, React maintains a virtual representation of the DOM - the Virtual DOM. When the component tree re-renders due to state or prop updates, React creates a new Virtual DOM Tree. Then, the reconciliation algorithm compares this new tree with the previous one to figure out the minimum number of read DOM operations needed to make the UI match the new state.
 2.  **Diffing Algorithm (O(n))**
	  Instead of comparing every node recursively (which would be O(n^3)), React uses heuristics:
	- If elements have different types, React destroys the old tree and builds a new one
	- If elements have the same type, React reuses the existing DOM node and only updates the changed attributes
	- When dealing with lists, React uses keys to identify which elements have changed, been added, or removed. Keys help React avoid unnecessary re-renders or element reordering
3. **Fiber architecture (React 16+)**
	Since React 16, reconciliation has been implemented using the Fiber architecture. A Fiber is a unit of work - it allows React to:
	- Pause, resume, and prioritize rendering work
	- Perform incremental rendering, which improves performance and responsiveness (esp. for animations and large updates)
4.  **Practical example**
	Suppose a list of 10 items changes because one time in the middle updates:
	- Without reconciliation, React would re-render the entire list in the DOM
	- With reconciliation, React compares keys, sees that only one item changed, and updates just that element - improving performance significantly.

**Q: What's the difference between `useMemo` and `useCallback`?**

 `useMemo` memoizes the **result** of a computation, while `useCallback` memoizes the function reference itself. Both help avoid unnecessary re-renders.