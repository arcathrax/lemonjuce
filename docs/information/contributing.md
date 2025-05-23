# Contributing

Welcome! Our goal is to provide clear, practical, and a self-contained documentation for JUCE development. Your contributions are vital to making that happen.

## Why Contribute?

lemonjuce aims to bridge the gap between the powerful capabilities of JUCE and the sometimes-opaque nature of its documentation. By contributing, you'll:

- **Improve your own understanding**: Explaining concepts helps solidify them in your mind.
- **Help others**:  Share your knowledge and make JUCE development more accessible to everyone.
- **Shape lemonjuce**: Help us define the scope and quality of our documentation.

## How to Contribute

We welcome contributions in various forms:

- **Writing Documentation Pages**: This is our primary need.  See "Style Guide" below for formatting guidelines.
- **Fixing Typos and Errors**: Even small corrections make a big difference.
- **Improving Examples**: Clear, concise examples are invaluable.
- **Suggesting New Topics**: Let us know what you'd like to see covered.
- **Reporting Issues**:  If you find something unclear or incorrect, please report it!

## Getting Started

- **Fork the Repository**: Go to [https://github.com/arcathrax/lemonjuce](https://github.com/arcathrax/lemonjuce) and click the "Fork" button.

- **Clone Your Fork**: Clone your forked repository to your local machine:
```bash
git clone git@github.com:<your_username>/lemonjuce.git
cd lemonjuce
```

- **Create a Branch**: Create a new branch for your changes. This keeps your work isolated and makes it easier to review. Use descriptive names!
```bash
git checkout -b my-new-feature-or-fix
```

- **Make Your Changes**: Edit the Markdown files in the `docs/` directory. (See "Style Guide" below).
- **Commit Your Changes**: Commit your changes with clear and concise commit messages.
```bash
git add .
git commit -m "Fix: Corrected typo in LookAndFeel documentation"
# or
git commit -m "Feat: Documentation for CustomLookAndFeel class"
```

6.  **Push to Your Fork**: Push your branch to your forked repository on GitHub.
```bash
git push origin my-new-feature-or-fix
```

7.  **Create a Pull Request**: Go to your forked repository on GitHub and click the "Create Pull Request" button.  Provide a detailed description of your changes, explaining *why* they are valuable.


## Style Guide

To ensure consistency and readability, please follow these guidelines:

- **Markdown Formatting**: Use standard Markdown syntax.
- **Headings**: Use clear and descriptive headings (e.g., `# Creating a Custom LookAndFeel`, `## Implementation`).
- **Code Blocks**:  Use fenced code blocks with the appropriate language identifier (e.g., ```cpp for C++ code).
- **Images**: Images should be hosted on GitHub or linked from external sources. Use descriptive alt text for accessibility.
- **Links**: Link to relevant JUCE documentation and other resources whenever possible.  Use meaningful link text.
- **Tone**: Write in a clear, concise, and friendly tone. Assume the reader has some basic JUCE knowledge but may be struggling with specific concepts. *Explain the "why" as much as the "how."*
- **Examples**: Provide practical examples that illustrate the concepts being explained.  Keep examples short and focused.
- **Consistency**: Follow the existing style of lemonjuce documentation. Look at other pages for inspiration.

## Commit Message Conventions

We follow these conventions to keep our commit history clean and understandable:

- **Prefix**: Use a prefix to indicate the type of change (e.g., `feat`, `fix`, `refactor`, `style`).
- **Scope**: Specify the area of the project affected by the change (e.g., `LookAndFeel`, `Graphics`).
- **Description**: Briefly describe the change in imperative mood (e.g., "Corrected typo", "Add documentation").

Examples: 

- `fix(creating_a_custom_look_and_feel.md): Corrected typo in drawRotarySlider function`
- `feat(creating_a_custom_look_and_feel.md): Create file`
- `feat(installation.md): Wrote "Creating an Application" section`
- `feat(contributing.md): Created file and wrote initial sections`


## Contact
For questions or discussions, please open an issue on GitHub.

We look forward to your contributions!
