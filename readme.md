## HTMX Training Wiki for Python (FastAPI) Developers

**Welcome to your guide to mastering HTMX!** This wiki will equip you with the knowledge and skills to build dynamic and interactive web applications with Python and FastAPI. 

**What is HTMX?**

HTMX is a lightweight JavaScript library that empowers server-centric development by adding interactivity directly to your HTML. Think of it as superpowers for your static pages!

**Why use HTMX?**

* **Say goodbye to JavaScript fatigue:** Build complex interactions without writing tons of Javascript.
* **Performance boost:** No full page reloads – just smooth, targeted updates for a responsive user experience.
* **Maintainability magic:** Server-side logic keeps your code clean and organized.
* **SEO friendly:** Dynamic updates don't hurt your search engine ranking.

**Getting Started with HTMX:**

1. **Installation:**
    * Include the HTMX script in your HTML: `<script src="https://unpkg.com/htmx.org@1.8.4"></script>`.
    * Or use a CDN for easy access.

2. **Basic Usage:**
    * Declare HTML attributes like `hx-get`, `hx-post`, or `hx-put` on elements to trigger requests based on events.
    * Specify the `hx-target` to update with the server's response, keeping the rest of your page intact.

**Key Features:**

* **Request Attributes:**
    * Trigger requests with different HTTP methods: `hx-get`, `hx-post`, `hx-put`, `hx-delete`.
    * Define update targets: `hx-target`, `hx-swap` (replace), `hx-push` (append).
    * Control triggers: `hx-trigger` (click, submit, etc.).
* **Responses:**
    * HTMX automatically updates the DOM based on the server's response.
    * Partial updates and smooth transitions create a delightful user experience.
* **Server-Side Integration:**
    * HTMX seamlessly works with FastAPI.
    * Your FastAPI endpoints handle requests and return tailored HTML snippets for updates.

**Examples with FastAPI:**

**1. Modal Dialog with Form Submission:**

* **HTML:**

```html
<button hx-get="/open-modal" hx-target="#modal-container">Open Modal</button>

<div id="modal-container" hx-swap>
  </div>

<template id="modal-template">
  <form hx-post="/submit-form">
    </form>
</template>
```

* **FastAPI Endpoint:**

```python
@app.get("/open-modal")
def open_modal():
  return templates.TemplateResponse("modal_template.html")

@app.post("/submit-form")
def submit_form(form_data: dict = Depends()):
  # Process form data and handle success/error scenarios
  # Return updated content for the modal container
  return {"message": "Form submitted successfully!"}
```

**2. Dynamic Data List with Pagination:**

* **HTML:**

```html
<ul id="data-list">
  </ul>

<button hx-get="/load-more" hx-target="#data-list" hx-append>Load More</button>

<div hx-include="/get-pagination"></div>
```

* **FastAPI Endpoints:**

```python
@app.get("/load-more")
def load_more_data(page: int = 1):
  # Fetch data for the requested page
  return {"data": new_data_items, "page": page + 1}

@app.get("/get-pagination")
def get_pagination(page: int = 1):
  # Generate pagination HTML based on current page and total pages
  return templates.TemplateResponse("pagination_template.html", {"page": page})
```

**Additional Features:**

* **Loading Indicators:** `hx-indicator` keeps users informed during requests.
* **Error Handling:** Gracefully handle errors with `hx-error`.
* **WebSockets and Server-Sent Events:** Real-time data updates are a breeze.
* **Custom JavaScript:** Extend HTMX with your own logic for advanced interactions.

**Resources:**

* HTMX Official Website: [https://htmx.org/docs/](https://htmx.org/docs/)
* FastAPI Documentation: [URL fastapi docs ON Tiangolo.com fastapi.tiangolo.com
