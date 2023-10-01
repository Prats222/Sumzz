# Sumzz https://sumzz-kqrvv11jk-prats222.vercel.app/

Hero.jsx

This component represents the hero section at the top of the web page.
It contains the project logo, a "GitHub" button, and some descriptive text.
When the "GitHub" button is clicked, it opens a new tab with the GitHub repository for the project.
This component is responsible for displaying basic information about the application.


### Demo.jsx:

#### State Management:
- `useState` and `useEffect` hooks from React are used to manage component-level state.
  - `article` state stores the current article's URL and summary.
  - `allArticles` state stores an array of previously entered articles.
  - `copied` state is used to provide visual feedback when copying article URLs.
  - `summaryCopied` state is used to provide visual feedback when copying article summaries.

#### API Request:
- `useLazyGetSummaryQuery` hook is imported from the `articleApi` (defined in `Article.js`).
- It is used to make asynchronous API requests for article summaries.
- `isFetching` indicates whether an API request is in progress.
- `error` stores any error messages received from the API.

#### Component Rendering:
- The component renders a form with an input field for entering article URLs.
- When the form is submitted, it calls the `handleSubmit` function.

#### Form Submission:
- `handleSubmit` function:
  - Prevents the default form submission behavior.
  - Checks if the entered article URL is in the list of previously entered articles.
  - If the article URL is found in the history, it sets the current article state to the previously saved article.
  - If the article URL is not in the history, it sends an API request to summarize the article.
  - If the API response contains a summary, it updates the state and local storage with the new article.

#### Copying Article URL:
- `handleCopy` function:
  - Sets the `copied` state to the URL being copied.
  - Uses the Clipboard API to copy the URL to the clipboard.
  - Clears the `copied` state after 3 seconds to provide visual feedback.

#### Browsing History:
- Displays a list of previously entered article URLs in a scrollable container.
- Each URL is clickable, allowing users to view the summary of that article.
- Each URL also has a "Copy" button that triggers the `handleCopy` function to copy the URL to the clipboard.

#### Displaying Article Summaries:
- If an API request is in progress (`isFetching` is true), a loading spinner is displayed.
- If an API request returns an error, an error message is displayed.
- If an article summary is available, it is displayed along with a "Copy Summary" button.
- Clicking the "Copy Summary" button triggers the `handleCopySummary` function to copy the summary to the clipboard.

### Article.js:

#### API Configuration:
- `createApi` function from Redux Toolkit is used to create the `articleApi`.
- The `baseQuery` configuration sets the base URL and headers for API requests.
- It includes the RapidAPI key and host as headers.

#### API Endpoints:
- The `articleApi` defines one endpoint named `getSummary`.
- The `getSummary` endpoint is a query function that takes article URL as a parameter and returns a summarized version of the article.

### store.js:

#### Redux Store Configuration:
- The Redux store is configured using `configureStore` from Redux Toolkit.
- The `articleApi` reducer is integrated into the store using the `[articleApi.reducerPath]` property.
- Middleware is added to the store to handle API requests and responses.

### Interaction Overview:

1. When a user enters an article URL and submits the form in `Demo.jsx`:
   - The `handleSubmit` function is called.
   - It checks if the URL is in the browsing history.
   - If not, it sends an API request using `useLazyGetSummaryQuery`.
   - If the API returns a summary, the state and local storage are updated.

2. The browsing history displays previously entered URLs, and users can click them to view summaries or copy them.

3. When copying an article URL or summary, the `handleCopy` or `handleCopySummary` functions are triggered, respectively.

4. The Redux store, configured in `store.js`, manages the state related to API requests and responses.

In summary, `Demo.jsx` is the main component responsible for user interactions and displaying content. `Article.js` configures the API endpoint, and `store.js` configures the Redux store to manage API-related state. Together, they allow users to enter article URLs, summarize articles, view summaries, and manage a browsing history.



### Main.jsx:

#### ReactDOM Rendering:
- `Main.jsx` serves as the entry point of your React application.
- It uses `ReactDOM.createRoot` and `render` to render the application inside a specific DOM element with the ID "root."

#### Provider and Store Integration:
- `Provider` from `react-redux` is used to wrap the entire application.
- The `store` created in `store.js` is passed as a prop to the `Provider` component.
- This integration provides access to the Redux store to all components within the application.

#### App Component Rendering:
- The `App` component is the main application component and is rendered within the `Provider`.
- It is wrapped in `React.StrictMode` for development mode checks and warnings.
- This component is where the core logic and UI of your application reside.

#### Interaction with Redux Store:
- The `store` passed via `Provider` allows the `App` component and its child components to interact with the Redux store.
- Actions, reducers, and middleware defined in the store are accessible for managing state and making API requests.

#### Application Initialization:
- When the application starts, `Main.jsx` is responsible for rendering the initial UI by rendering the `App` component.
- This initializes the application's UI and sets up the Redux store for state management.

In summary, `Main.jsx` is responsible for initializing and rendering your React application. It integrates the Redux store using the `Provider` component, making the store and its features available throughout the application. The core logic of your application is contained within the `App` component, which is rendered within `Main.jsx`.
 
