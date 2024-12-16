Here is a story, you build a reusable code and someone asks you to build a new feature in that code and you do it. So there might be a lot of such feature addition which will make that previously reusable code hard to maintain. Issues like:
-  Bundle size and performance
- Difficulties in maintenance
- Implementation complexity
- API complexity

One Principle to fix that is **Inversion of Control**. According to wikipedia:
> ...in traditional programming, the custom code that expresses the purpose of the program calls into reusable libraries to take care of generic tasks, but with inversion of control, it is the framework that calls into the custom, or task-specific, code.

It is like: Make your abstraction do less stuff and make your users do that instead. 
