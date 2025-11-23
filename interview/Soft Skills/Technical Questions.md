**Q: What type of code makes you angry?**
Code that is hard to read or maintain — for example, files with no structure, duplicated logic, or unclear naming. It slows the whole team down. I prefer clean, modular, and well-documented code.

**Q: What architecture would you choose for an app? Why?**
It depends on the project size. For small apps, a simple modular structure with feature folders works well. For larger apps, I prefer **feature-sliced design** or **Nx monorepos**, because they enforce boundaries and make scaling easier.

**Q: What's your favorite technology?**
React with TypeScript. React gives flexibility and a strong ecosystem, and TypeScript improves safety and developer experience by catching errors early.

**Q: Is there anything you would still like to learn? Are you learning anything new now? Why is it interesting for you?**
Yes, I’m currently improving my knowledge of **performance optimization** in React apps and exploring **micro-frontends**. I find it interesting because it helps build scalable apps for larger teams.

**Q: What styling approach would you prefer and why?**
I prefer **Tailwind CSS** for utility-first styling and **ShadCN** when building modern UI quickly. For large-scale projects, I also see value in CSS Modules for maintainability.

**Q: Have you dealt with code review?**
Yes, regularly. I see it as both a way to maintain quality and share knowledge across the team. I try to give constructive feedback and also learn from others’ approaches.

**Q: Do you have experience in pair programming? Have you divided tasks with other developers?**
Yes, I’ve done pair programming when solving complex bugs or onboarding new team members. I’ve also split features into smaller tasks so different developers could work in parallel without conflicts.

**Q: Have you ever worked with legacy code?**
Yes, and I know it can be challenging. My approach is to first add tests to ensure stability, then gradually refactor in small steps while keeping the system functional.

**Q: How would you increase (improve) the quality of the code?**
By enforcing code reviews, using linters/formatters, writing tests, and keeping documentation up to date. Also, by discussing architecture decisions early so we avoid future rework.

**Q: How have you been automating the processes for processing large amounts of data?**
On the frontend, I’ve used **pagination, virtualization, and lazy loading** to handle large datasets efficiently. On the backend side, I collaborated with developers to ensure APIs supported filtering and batching.

**Q: Do you have the experience starting a project from scratch?**
Yes, I’ve set up projects from scratch using React + TypeScript, configured ESLint/Prettier, set up testing libraries, and structured features with FSD (feature-sliced design) for scalability.

**Q: What solution will you pick: fast or with good quality?**
I aim for a balance. If speed is critical, I deliver a working MVP but still keep the structure clean enough to extend later. For long-term projects, I prioritize quality to avoid technical debt.

**Q: What would you improve on your latest project if you'll have the possibility?**
I’d add more **E2E testing** with Playwright, because it would reduce manual QA effort and catch regressions earlier.

**Q: What is a good test for you?**
A good test is simple, focused, and stable. It should test one specific thing, not rely on implementation details, and help prevent regressions.

**Q: What goes first: investigation or solution?**
Investigation always comes first. Without understanding the root cause, the solution might be wrong or incomplete.

**Q: What actually means to design responsive UI components using React concepts?**
It means building **reusable components** that adapt to different screen sizes by combining **props-driven design, CSS responsiveness (flex, grid, media queries), and sometimes hooks like `useWindowSize`**.

**Q: What is in your opinion an ideal coverage of the tests?**
There’s no magic number, but I’d say **70–80% coverage** is good if the critical paths are fully tested. It’s more important to cover core business logic and edge cases than to chase 100%.
