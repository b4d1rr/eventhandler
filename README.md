# eventhandler

A lightweight local simulation of a serverless event-handling environment.
This project provides a structured way to validate, normalize, and process JSON-based events using a Lambda-style `handler(event, context)` function.

---

## 📌 Overview

`eventhandler` enables you to:

* Run serverless-style event logic **locally**.
* Test event flows before deploying them to cloud services.
* Maintain consistent response formatting for all event types.
* Use a simple CLI utility (`run_local.py`) to execute event files.

The project includes example event templates and predefined handler stubs for common event categories.

---

## ✨ Features

* **Uniform Response Structure**
  Each handler returns:

  ```json
  {
    "status": "ok" | "error",
    "message": "...",
    "data": { ... } | null,
    "errors": [ ... ]
  }
  ```

* **Event Type Routing**
  Automatically dispatches based on:

  * `USER_SIGNUP`
  * `PAYMENT`
  * `FILE_UPLOAD`

* **Local Execution Tool**
  Run single or multiple events easily.

* **Clear Implementation Structure**
  Handlers are pre-scaffolded with TODO areas for business logic.

---

## 📂 Project Structure

```
eventhandler/
│
├── handler.py          # Core event handler with routing and validation
├── run_local.py        # CLI for executing event files locally
└── events/             # Example JSON event inputs
```

---

## 🧠 How It Works

### `handler.py`

Defines the main entry point:

```python
def handler(event: dict, context=None) -> dict
```

This function:

1. Validates the incoming event.
2. Confirms that the `type` field is present.
3. Routes the event to the correct handler:

   * `handle_user_signup`
   * `handle_payment`
   * `handle_file_upload`
4. Returns a standardized result dictionary.

Each sub-handler contains placeholder logic that you can extend.

---

### `run_local.py`

This script lets you test event flows without deploying anything.

#### Run a single event:

```bash
python run_local.py --event events/example.json
```

#### Run all events in the folder:

```bash
python run_local.py --all
```

---

## 📄 Example Event File

Create JSON files inside `events/`:

```json
{
  "type": "USER_SIGNUP",
  "user_id": 42,
  "email": "user@example.com",
  "plan": "premium"
}
```

---

## 🧪 Expected Output

A processed event will return something similar to:

```json
{
  "status": "ok",
  "message": "User signup processed successfully.",
  "data": {
    "user_id": 42,
    "email": "user@example.com",
    "plan": "premium"
  },
  "errors": []
}
```

If validation fails, a structured error response is returned.

---

## 🛠 Development Notes

Areas marked with `TODO` in `handler.py` indicate:

* Input validation requirements
* Normalization tasks
* Business logic you may add
* Additional data mapping

You may extend event types or modify routing as needed.

---

## 🤝 Contributing

Feel free to submit issues, suggestions, or pull requests via GitHub.
