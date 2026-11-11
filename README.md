# Quiz CLI

## Overview

Quiz CLI is an interactive terminal quiz game for learning JavaScript, Node.js, and general programming concepts. It loads quiz content from a local JSON file, presents multiple-choice questions, tracks the score, and displays explanations and a review of incorrect answers.

The application is implemented with Node.js ES modules and Node.js built-in modules. It has no third-party runtime dependencies.

## Features

- Choose from three quiz categories: JavaScript Basics, Node.js Fundamentals, and General Programming.
- Play all questions in a category, or select a shorter quiz when the category contains enough questions.
- Randomize question order for each quiz.
- Validate numeric menu selections and allow the player to continue through the quiz at their own pace.
- Show correctness feedback, answer explanations, quiz progress, score, and a final performance message.
- Review incorrect answers and their correct choices at the end of a quiz.
- Replay without restarting the process.
- Colorize terminal output using ANSI escape codes; no color package is required.

## Architecture

The application is a small, local command-line program:

1. `test-app/index.js` loads `test-app/data/questions.json` and runs the interactive application loop.
2. `test-app/src/input.js` wraps Node.js `readline` to provide prompts, numbered selection, confirmation, and pause helpers.
3. `test-app/src/quiz.js` shuffles the selected questions, tracks answers and score, presents questions, and renders results.
4. `test-app/src/colors.js` supplies ANSI-based terminal styling.

Quiz data is stored in JSON and read from disk at startup. The repository contains no server, external API integration, or database configuration.

## Technology Stack

| Technology | Use |
| --- | --- |
| JavaScript (ES modules) | Application implementation |
| Node.js | Runtime (version 18 or newer) |
| Node.js built-ins | File access (`node:fs/promises`), paths (`node:path`), URL utilities (`node:url`), terminal input (`node:readline`), and test runner (`node --test`) |
| JSON | Quiz category and question data |

## Repository Structure

```text
.
├── README.md
└── test-app/
    ├── package.json          # Project metadata, runtime requirement, and npm scripts
    ├── index.js              # CLI entry point and application loop
    ├── data/
    │   └── questions.json    # Categories, questions, choices, answers, and explanations
    └── src/
        ├── colors.js         # ANSI terminal color helpers
        ├── input.js          # Interactive terminal input helpers
        └── quiz.js           # Quiz state, question flow, and result display
```

The repository also contains `.DS_Store` and `__MACOSX` entries, which are macOS/archive metadata and are not used by the application.

## Prerequisites

- Node.js 18.0.0 or later.
- A terminal capable of running an interactive Node.js process. ANSI color support depends on the terminal.

No separate database, service, or global package installation is required.

## Installation

Clone or download the repository, then enter the application directory:

```sh
cd test-app
```

There are no declared third-party dependencies, so `npm install` is not required for the current project.

## Configuration

There is no separate configuration file or configuration command. The question bank is maintained in `data/questions.json`. The application expects that file to contain a `categories` object whose category entries have a `name` and a `questions` array. Each question uses `question`, `options`, and `answer` fields; `explanation` is displayed when present. The `answer` value is a zero-based index into `options`.

### Environment Variables

No environment variables are read by the application.

## Running the Application

From the repository root:

```sh
cd test-app
npm start
```

This runs the `start` script defined in `test-app/package.json` (`node index.js`). You can also run the program directly from the `test-app` directory:

```sh
node index.js
```

Follow the terminal prompts to select a category, choose the number of questions, enter the number corresponding to an answer, and decide whether to play again.

## Usage Examples

The menu choices are generated from the categories in `data/questions.json`. The bundled data includes JavaScript Basics, Node.js Fundamentals, and General Programming, with five questions in each category. The count menu therefore offers all questions, three questions, or five questions.

An interaction proceeds through these steps:

1. Choose a category by entering its displayed number.
2. Choose the quiz length by entering its displayed number.
3. Press Enter to start, then select each answer using its displayed number.
4. Review feedback and the final score; optionally play another quiz.

Questions are shuffled, so their order can vary between runs.

## API Documentation

This repository provides an interactive CLI, not an HTTP service or public web API. Its internal JavaScript modules export the following helpers:

- `src/input.js`: `createInterface`, `prompt`, `select`, `confirm`, and `pressEnter`.
- `src/colors.js`: `colorize` and convenience styling functions such as `success`, `error`, and `info`.
- `src/quiz.js`: the `Quiz` class.

These are internal application modules; the repository does not document a separately versioned public library API.

## Database Information

No database is used. Quiz content is loaded from the local JSON file `data/questions.json`.

## Build Instructions

No build or compilation step is defined. Node.js executes the ES module source directly. Run the application with `npm start` from `test-app/`.

## Testing

The package defines this test command:

```sh
cd test-app
npm test
```

It runs Node's built-in test runner using `node --test`. No test files are present in the repository, so automated test coverage is not supplied here.

## Deployment

No deployment configuration, container definition, or release workflow is present. This is a local CLI application; run it in an environment with Node.js 18 or newer and the repository files available.

## CI/CD

No CI/CD workflow files are present in the repository.

## Troubleshooting

- **Node.js version error or unsupported syntax:** Confirm that Node.js 18 or newer is installed (`node --version`).
- **Question data cannot be loaded:** Run the program from the repository's `test-app/` directory and ensure `test-app/data/questions.json` exists and contains valid JSON. The entry point resolves the data file relative to its own location.
- **Menu selection is rejected:** Enter a displayed option number within the range shown by the prompt.
- **No terminal colors:** The program uses ANSI escape codes; behavior depends on the terminal's ANSI support.

## Contributing

No contribution guidelines are provided in the repository. When making changes, keep quiz content in `test-app/data/questions.json` and application behavior in the corresponding source modules. Run `npm test` from `test-app/` after changes (the repository currently contains no test files).

## License

`test-app/package.json` declares the project license as MIT. A separate license text file is not present in the repository.

## Additional Notes

The package is named `quiz-cli` and is version `1.0.0` in `test-app/package.json`; the repository is titled `test-app`. The package metadata describes the project as an interactive command-line quiz game for learning JavaScript.