# Alrwad University Platform (Lite)

## Introduction

This is a prototype for "Alrwad University Lite," an all-in-one platform designed to help students manage their academic life. This Lite version focuses on core student-facing features, including a dashboard, course browsing, assignment tracking, and an AI-powered schedule generator.

The application is built to be responsive, supports dark/light modes, and includes basic LTR/RTL direction switching for English and Arabic language interfaces (note: full Arabic text translation is not implemented; the switch primarily handles UI direction and sample text).

## Tech Stack

*   **Framework:** Next.js 15 (App Router)
*   **Language:** TypeScript
*   **UI Library:** React 18
*   **Components:** ShadCN UI
*   **Styling:** Tailwind CSS
*   **AI Integration:** Genkit (using Google Gemini models)
*   **Icons:** Lucide React
*   **Fonts:** Cairo (for Arabic and Latin characters)

## Key Features Implemented (Lite Version)

*   **Public Area:**
    *   Homepage with feature overview.
    *   Login & Registration pages (UI and conceptual navigation only; no actual authentication).
*   **Authenticated Student Area:**
    *   **Dashboard:**
        *   Academic Setup Wizard (specialization, level, term selection; data stored in `localStorage`).
        *   Display of selected academic profile and enrolled dummy courses.
        *   Summary cards (My Courses, Upcoming Deadlines, Recent Announcements - dummy data).
        *   Assignments Overview Chart (using `recharts` via ShadCN, dummy data).
        *   Quick Links to other sections.
    *   **Course Browsing:**
        *   Displays a list of dummy courses with details.
        *   Modal to view detailed information for each course.
    *   **Assignments List:**
        *   Tabbed view for "Upcoming & Overdue" and "Submitted & Graded" assignments (dummy data).
        *   "Submit Work" dialog (conceptual submission, client-side status update).
        *   "View Submission Details" dialog for submitted/graded items.
    *   **AI Schedule Generator:**
        *   Utilizes a Genkit flow (`generateScheduleFlow`) connected to Google's Gemini model.
        *   Interface to input schedule preferences (text-based).
        *   Displays the AI-generated weekly schedule.
        *   Includes AI assistance messages if provided by the model.
    *   **Messages Page:**
        *   Conceptual messaging interface (UI only).
        *   Selectable contacts list (dummy data).
        *   Chat area that updates based on selection.
        *   Message input and "send" functionality (client-side UI updates and toast notifications).
    *   **Profile Page:**
        *   Displays dummy student profile information.
        *   "Edit Profile" mode allowing client-side modification of certain fields (no backend persistence).
    *   **Settings Page:**
        *   Dark/Light Mode toggle (persisted in `localStorage`).
        *   Language & Direction toggle (English LTR / Arabic RTL, persisted in `localStorage`).
        *   Conceptual notification preferences (UI toggles, persisted in `localStorage`).
*   **General UI/UX:**
    *   Responsive design for various screen sizes.
    *   Collapsible sidebar navigation.
    *   Header with theme and language controls.
    *   Toast notifications for user feedback.

## Project Structure Overview

*   `src/app/`: Contains all the application routes and layouts.
    *   `layout.tsx`: The root layout, setting up the base HTML structure and font.
    *   `globals.css`: Global styles and ShadCN UI theme variables.
    *   `(main)/`: Route group for the authenticated part of the application (dashboard, courses, etc.).
        *   `layout.tsx`: Layout for authenticated pages, includes the sidebar and main header.
        *   `dashboard/page.tsx`, `courses/page.tsx`, etc.: Individual page components.
    *   `(public)/`: Route group for public-facing pages.
        *   `layout.tsx`: Layout for public pages, includes a simpler public navbar.
        *   `page.tsx`: The main homepage content.
        *   `login/page.tsx`, `register/page.tsx`: Login and registration pages.
*   `src/components/ui/`: Reusable UI components, primarily from ShadCN UI.
*   `src/ai/`: Genkit related files.
    *   `genkit.ts`: Genkit initialization and configuration.
    *   `dev.ts`: File for importing flows for Genkit's dev UI.
    *   `flows/`: Directory for Genkit AI flows.
        *   `generate-schedule-flow.ts`: The AI flow for generating student schedules.
*   `src/lib/`: Utility functions (e.g., `cn` for classnames).
*   `src/hooks/`: Custom React hooks (e.g., `useToast`, `useIsMobile`).
*   `public/`: Static assets like images (e.g., `Al_Rowad_University_Logo.png`).
*   `next.config.ts`: Next.js configuration.
*   `tailwind.config.ts`: Tailwind CSS configuration.
*   `components.json`: ShadCN UI configuration.

## Getting Started / Running Locally

### Prerequisites

*   Node.js (v18 or later recommended)
*   npm or yarn

### Setup

1.  **Clone the repository** (if applicable, or use the provided project files).
2.  **Install dependencies:**
    ```bash
    npm install
    # or
    yarn install
    ```
3.  **Set up Environment Variables:**
    This project uses Genkit with Google's Gemini models for AI features. You'll need a Google API key.
    Create a file named `.env.local` in the root of your project and add your API key:
    ```env
    GOOGLE_API_KEY=YOUR_GEMINI_API_KEY
    ```
    Replace `YOUR_GEMINI_API_KEY` with your actual API key. You can obtain one from [Google AI Studio](https://aistudio.google.com/app/apikey).

4.  **Run the Genkit Developer UI (optional but recommended for AI development):**
    This allows you to inspect and test your Genkit flows.
    ```bash
    npm run genkit:dev
    # or
    yarn genkit:dev
    ```
    This will typically start the Genkit UI on `http://localhost:4000`.

5.  **Run the Next.js Development Server:**
    ```bash
    npm run dev
    # or
    yarn dev
    ```
    The application should now be accessible at `http://localhost:9002` (or the port specified in your `package.json` dev script).

## AI Features (Genkit)

The primary AI feature implemented is the **AI Schedule Generator**, located in `src/ai/flows/generate-schedule-flow.ts`.
*   It uses `ai.defineFlow` and `ai.definePrompt` from Genkit.
*   Input and output schemas are defined using Zod.
*   The prompt guides the Gemini model to generate a weekly schedule based on user preferences.
*   You can test this flow independently using the Genkit Developer UI (if running `genkit:dev`) by navigating to the `scheduleGeneratorFlow` and providing input.

## Customization

*   **Theming:** Colors and styles are primarily controlled by CSS variables in `src/app/globals.css`. These variables are used by Tailwind CSS and ShadCN UI components.
*   **Adding New Pages:** Create new directories and `page.tsx` files within the `src/app/(main)/` or `src/app/(public)/` route groups.
*   **Modifying UI Components:** Edit the respective `.tsx` files in `src/app/` or `src/components/ui/`.

## Limitations of this Prototype

*   **No Backend Database/Authentication:** User data, courses, assignments, etc., are mostly hardcoded dummy data or stored client-side in `localStorage`. There is no actual backend database or authentication system.
*   **Conceptual Features:** Some features like "submitting assignments," "sending messages," or "saving profile changes" are UI-only and do not interact with a backend.
*   **Limited AI Sophistication:** The AI schedule generator is a basic implementation. More advanced error handling, conflict resolution, and constraint management would be needed for a production system.
*   **Basic RTL/Language Support:** The language switch primarily toggles text direction (LTR/RTL) and updates sample text. Full localization and translation of all content would require a dedicated i18n library (e.g., `next-intl`).
*   **Error Handling:** While some basic error handling is in place (e.g., for AI flow calls), comprehensive error management across the application is not fully implemented.

This README provides a snapshot of the "Alrwad University Lite" prototype.
link of project:

https://9000-firebase-studio-1747333510552.cluster-axf5tvtfjjfekvhwxwkkkzsk2y.cloudworkstations.dev
```
