# SmartLoans

## Live Demo

[View the live app](https://ramona-dsouza.github.io/Finance-Smart-Loan-Calculator/)

## Overview

SmartLoans is a single-page loan calculator that computes monthly payment, total payment, and total interest from principal, annual interest rate, and term. It is implemented as a static web application with no build step or backend, emphasizing clear state feedback, accessibility, and a minimal interaction path.

## Concept

The project applies a systems view to a focused financial tool: treat the calculator as one input-to-output pipeline with explicit states (idle, loading, results, error) and a single primary action. UX choices are informed by principles carried over from immersive interfaces—where feedback and state must be unambiguous and immediate—translated to the web: a loading state during computation, results surfaced in place, and inline error handling that does not rely on modal blocking. The implementation stays framework-free to keep the relationship between user input, calculation logic, and DOM updates explicit and auditable.

## Technical Architecture

- **Stack:** Vanilla JavaScript, HTML5, Bootstrap 4 (CSS/JS via CDN), jQuery (DOM and events). No bundler or package manager; the app runs from static files.
- **Structure:** Single `index.html` (markup and layout), single `app.js` (event handling and calculation). Form and results live in one view; visibility is toggled by script.
- **Calculation:** Standard monthly payment formula: `M = P * [r(1+r)^n] / [(1+r)^n - 1]`, with `P` = principal, `r` = monthly rate (annual rate / 12), `n` = number of payments (years × 12). Total payment and total interest are derived from the resulting monthly value.
- **State:** Submit triggers a 2-second loading state (loader shown, results hidden); on completion, results are shown and loader hidden. Invalid or missing input triggers an inline error message that auto-clears after 3 seconds. No persistent storage; all state is in the DOM and in-memory variables.

## Interaction Model

1. **Input:** User enters loan amount, interest rate (percent), and years to repay in the form and submits.
2. **Loading:** Form remains visible; a loading indicator is shown and results are hidden for the duration of the calculation delay.
3. **Results:** Monthly payment, total payment, and total interest are displayed in disabled fields directly below the form. The loader is hidden.
4. **Error:** If inputs are missing or do not yield a finite result, an alert is inserted above the form title, then removed after 3 seconds. Results and loader are both hidden.
5. **Re-run:** User can change inputs and submit again; each submit resets the results view and runs the same flow.

Accessibility is addressed via semantic form structure, `aria-label` on result fields, and a layout that works across viewport sizes (Bootstrap responsive grid).

## Setup

No build or install step. Serve the project root over HTTP (or open `index.html` in a browser; some environments may restrict file access for local scripts).

1. Clone or download the repository.
2. Ensure `img/loading.gif` exists if the loading state is desired; otherwise the loading block may be empty.
3. Open `index.html` in a browser or serve the folder with any static server (e.g. `npx serve .`, or your editor’s live server).

Dependencies (Bootstrap, jQuery, Popper) are loaded from CDNs in the HTML; no `package.json` or `node_modules` are required.

## Purpose

This project demonstrates a self-contained financial calculator with a clear separation between input capture, business logic (amortization math), and presentation. It is suitable for portfolios as an example of systems thinking (single pipeline, explicit states), UX translation from high-feedback immersive contexts to the web (loading and error states, in-context results), and straightforward technical implementation without frameworks.
