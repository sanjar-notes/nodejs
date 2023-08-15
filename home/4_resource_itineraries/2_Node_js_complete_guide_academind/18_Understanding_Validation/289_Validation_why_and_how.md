# 289. Validation, why and how
Created Monday 14 August 2023 at 11:17 pm


## What and why validation
- What - Validation in context of backend app means making sure that the data accepted from the client is correct and in the expected format.
- Why - to make sure the database (app data) is in the correct state.

Of course, what is valid or not is a product level decision

## How is validation done
The server gets some input in a request, it checks (validates) the data, the data is accepted (stored/processed) if valid, else the server raises an error.


## Validation goals of a BE app
- A major goal of backend apps is to make sure the data they take from the user (via forms, or otherwise too) is in the correct format and semantically valid.
- Another goal is to sanitize the input against security vulnerabilities like XSS, SQLI.


## What happens if validation is absent
- Validation is important since wrong data can lead to the system/app (BE + FE) being in the wrong state - this can be a minor issue or a very big problem (if lots of data is in bad state, and corrective data has been lost).
