Execution Flow in Angular 20 (Standalone App)
Here's how Angular 20 executes your app — step by step, including what index.html, main.ts, and your root standalone component (like App) do.

🚦 1. index.html — The Static HTML Shell

<!-- src/index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>My Angular 20 App</title>
  <base href="/" />
</head>
<body>
  <app-root></app-root> <!-- This tag is where Angular inserts your root component -->
</body>
</html>
✅ What Happens:
The browser loads this as the entry point.

It contains a placeholder <app-root> where Angular will render your app.

It includes a <script src="main.js"> (automatically added by Angular CLI).

🛠 2. main.ts — The Application Bootstrap File
ts

// src/main.ts
import { bootstrapApplication } from '@angular/platform-browser';
import { App } from './app/app';
import { appConfig } from './app/app.config';

bootstrapApplication(App, appConfig)
  .catch((err) => console.error(err));
✅ What Happens:
bootstrapApplication() is a new, simplified alternative to bootstrapping with NgModule.

You give it your standalone root component (App) and an optional app configuration object.

It tells Angular:

“Start the app by rendering App inside <app-root> using this config.”

🧱 3. App (a Standalone Component) — The Root UI Element
ts

// src/app/app.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  standalone: true,
  template: `<h1>Hello Angular 20!</h1>`
})
export class App {}
✅ What Happens:
This component is marked with standalone: true, so it doesn't need to be declared in an NgModule.

Angular uses the selector: 'app-root' to find <app-root> in index.html.

The component's HTML replaces that tag in the DOM.

🧩 4. app.config.ts — Optional App-Level Providers
ts

// src/app/app.config.ts
import { ApplicationConfig } from '@angular/core';
import { provideHttpClient } from '@angular/common/http';
import { provideRouter } from '@angular/router';
import { routes } from './app.routes';

export const appConfig: ApplicationConfig = {
  providers: [
    provideHttpClient(),
    provideRouter(routes)
  ]
};
✅ What Happens:
This replaces the role of AppModule's providers.

You configure services like:

Routing

HTTP

Interceptors

Global providers (e.g., injectors, guards)

🔁 Execution Flow Summary in Angular 20
1. 🔵 index.html
Browser loads the static HTML page

Contains <app-root> as a placeholder

2. 🔵 main.ts
Entry point of Angular app

Calls bootstrapApplication(App, appConfig)

Starts Angular runtime and sets up DI

3. 🔵 App (Standalone Component)
Angular renders it inside <app-root>

Its template becomes visible on screen

4. 🔵 app.config.ts
Provides optional services (HTTP, routing, etc.)

Replaces traditional NgModule configuration

🚀 Diagram: Angular 20 Execution Flow (Standalone Style)

index.html
  └── <app-root>
         ↓
main.ts → bootstrapApplication(App, appConfig)
         ↓
App (standalone component)
         ↓
template gets rendered in place of <app-root>
         ↓
app.config.ts provides services like router, http, etc.
