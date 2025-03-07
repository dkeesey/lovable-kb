# Prompt Engineering for Lovable

List of prompting strategies and approaches to get the most out of Lovable.

## Basics

Prompts are the primary way to interact with Lovable app:

1. **Welcome Screen**: Start with prebuilt prompts or create your own.
2. **Builder UI**: Use the chat-based interface to iterate quickly.

Prompts serve as the backbone of all interactions.

## Prompting Strategies

These strategies will often work combined, depending on your specific use cases. Feel free to experiment with them and see which ones give the best results.

### Contextual Prompting

Providing context can help Lovable understand the broader scope of your requirements. Before asking for specific tasks, you can set the stage with background information.

**Setting the context**

```
We are building a project management tool that helps teams track their tasks.
This tool should have features like:
 - user authentication
 - project creation
 - task assignments
 - reporting

Now, for the first task, create the UI for project creation.
```

**Another example:**

```
I need a CRM app with Supabase integration and a secure auth flow. Start by setting up the backend.
```

### Incremental Prompting

Our experience has shown that making incremental, smaller changes will yield better results than dumping a huge prompt and expecting AI to handle it well.

**DON'T**:

```
Build a CRM app with Supabase, auth, Google Sheets export, and data enrichment.
```

**DO**:

```
Set up a Supabase-connected CRM backend.
```
```
Great! Could you please add a secure authentication flow with user roles?
```
```
Thank you! The next step is to integrate Google Sheets to export records.
```

### Using Image Prompts

You as a user can upload images with your prompt and ask Lovable to build a solution based on it.

**Simple image upload prompting**

```
Create and implement a UI that looks as similar as possible to the image attached.
```

**Image prompting with detailed instructions**

```
I want you to create the app as similar as possible to the one shown in this screenshot.
It's essentially a kanban clone.
It should have the ability to add new cards (tickets) in each column, have the ability to change the order of those tickets within a single column, and even move those cards between columns.
Feel free to use the Pangea home dnd npm package for drag-and-drop functionality.
```

### Feedback Integration

Review the AI's output and provide specific feedback for refinements.

```
The login form looks good, but please add validation for the email field to ensure it contains a valid email address.
```

### Avoid Ambiguity

Ensure your prompts are clear and unambiguous. Avoid vague terms and be as specific as possible about what you need.

**DON'T**:

```
Make this app better.
```

**DO**:

```
Refactor the app to clean up unused components and improve performance, without changing UI or functionality.
```

### Add Constraints

Sometimes, adding constraints can help focus the AI on what's important and avoid unnecessary complexity.

```
Create a simple to-do app with a maximum of 3 tasks visible at a time.
Include the ability to add, edit, and delete tasks.
```

### Be Nice!

Even though it may sound surprising, studies have shown that polite prompts with basic professional courtesy yield better results. This is because respectful prompts often include a few extra words, which provide more context for the AI.

## Advanced Prompting Strategies

### Emphasizing Accessibility

Encourage the generation of code that adheres to accessibility standards and modern best practices.

```
Generate a React component for a login form that follows accessibility best practices, including appropriate ARIA labels and keyboard navigation support.
```

### Predefined Components and Libraries

Specify the use of certain UI libraries or components to maintain consistency and efficiency in your project.

```
Create a responsive navigation bar using the shadcn/ui library with Tailwind CSS for styling.
```

### Implementing Chain of Thought (CoT) Prompts

For complex tasks, encourage the AI to process the problem step by step before providing a solution.

```
Let's think through the process of setting up a secure authentication system:
1. What are the necessary components?
2. How should they interact?
3. Provide the implementation code.
```

## Debugging and Issue Reporting

### Be Specific When Correcting Issues

Issues will happen, sometimes builds will fail and the app that was generated will not look exactly as you wanted it. Effective prompting can help you get back on track.

**Avoid generic and broad prompts**

```
Nothing works, fix it!
```

**Make your prompts more detailed and specific**

```
Now the screen has gone blank and I am no longer able to make edits.
Can you check what happened?
```

### Using Dev Console for Reporting Bugs

If you are more technical and an issue has happened, then pasting an error logged in the browser's Console can be very helpful.

```
My app is not working anymore and the screen is blank.
Here's the copy/paste from Dev tools console, can you fix the issue?

Error occurred:
TypeError: Q9() is undefined  at https://example.lovable.app/assets/index-DWQbrtrQQj.js
: 435 : 39117 index-DWQbrtrQQj.js:435:35112
onerror https://example.lovable.app/assets/index-DWQbrtrQQj.js:435
```

## Special Purpose Prompts

### Error Debugging

For minor errors:

```
The same error persists. Do not make any code changes yet—investigate thoroughly to find the exact root cause. Analyze logs, flow, and dependencies deeply, and propose solutions only once you fully understand the issue.
```

For major errors:

```
This is the final attempt to fix this issue. Stop all changes and methodically re-examine the entire flow—auth, Supabase, Stripe, state management, and redirects—from the ground up. Map out what's breaking and why, test everything in isolation, and do not proceed without absolute certainty.
```

### Refactoring

```
Refactor this file without changing the UI or functionality—everything must behave and look exactly the same. Focus on improving code structure and maintainability only. Document the current functionality, ensure testing is in place, and proceed incrementally with no risks or regressions.
```

### UI Design Changes

```
Make only visual updates—do not impact functionality or logic in any way. Fully understand how the current UI integrates with the app, ensuring logic, state management, and APIs remain untouched. Test thoroughly to confirm the app behaves exactly as before.
```

### Optimize for Mobile

```
Optimize the app for mobile without changing its design or functionality. Analyze the layout and responsiveness to identify necessary adjustments for smaller screens and touch interactions. Outline a detailed plan before editing any code, and test thoroughly across devices to ensure the app behaves exactly as it does now.
```

## Chat Modes

Chat modes are an experimental feature which allow you to switch how you interact with Lovable:

1. **Default**: Chat and make edits to your project.
2. **Chat only**: Chat without making edits to your project.
